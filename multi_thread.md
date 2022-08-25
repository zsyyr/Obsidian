- ![multithreads](/multithreads.jpeg)

- ![kernel_thread](/kernel_thread.jpg)

- ![thread_pool](/thread_pool.jpeg)
- [ThreadPoolExecutor](https://docs.python.org/3.10/library/concurrent.futures.html#concurrent.futures.ThreadPoolExecutor)
```
import concurrent.futures
import urllib.request

URLS = ['http://www.foxnews.com/',
        'http://www.cnn.com/',
        'http://europe.wsj.com/',
        'http://www.bbc.co.uk/',
        'http://some-made-up-domain.com/']

# Retrieve a single page and report the URL and contents
def load_url(url, timeout):
    with urllib.request.urlopen(url, timeout=timeout) as conn:
        return conn.read()

# We can use a with statement to ensure threads are cleaned up promptly
with concurrent.futures.ThreadPoolExecutor(max_workers=5) as executor:
    # Start the load operations and mark each future with its URL
    future_to_url = {executor.submit(load_url, url, 60): url for url in URLS}
    for future in concurrent.futures.as_completed(future_to_url):
        url = future_to_url[future]
        try:
            data = future.result()
        except Exception as exc:
            print('%r generated an exception: %s' % (url, exc))
        else:
            print('%r page is %d bytes' % (url, len(data)))
```
- [Semaphore Objects](https://docs.python.org/3.10/library/threading.html#semaphore-objects)
```
from threading import Semaphore
my_semaphore = Semaphore(2) #可设置信号量数量，增加并行度
my_semaphore.acquire()
task code
my_semaphore.release()
```
	- 信号量同步会增加等待开销，最好只在需要防止交叉运行的代码前后使用。
	- 只有信号量为1时才是原子操作，大于1则相应的code仍会穿插进行。