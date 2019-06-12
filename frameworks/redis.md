# Redis

## Redis基础

### 配置

* 远程连接：./redis-cli -h 127.0.0.1 -p 6379
  * CONFIG SET protected-mode no 或者修改配置文件中的 protected-mode
  * 测试环境中，可以重启redis server，设置redis-server --protected-mode
  * Setup a bind address：

    ```bash
    config set bind 192.168.1.100 10.0.0.1 #默认是bind 127.0.0.1
    ```

  * Setup an authentication password：`config set requirepass my_password,` 远程登录时：redis-cli -h 127.0.0.1 -p 6379 -a my\_password

### 数据类型与基本操作

{% embed url="https://blog.csdn.net/chen88358323/article/details/47318303" %}

## Scrapy redis

{% embed url="https://www.cnblogs.com/kylinlin/p/5198233.html" caption="参考文件" %}

重要组件：

* Scheduler
* dupefilter: RFPDupeFilter
* spider: RedisSpider
* RedisMixin
* RedisPipeline

### 源码解析

#### pipeline

```python
class RedisPipeline(object):
    """Pushes serialized item into a redis list/queue

    Settings
    --------
    REDIS_ITEMS_KEY : str
        Redis key where to store items.
    REDIS_ITEMS_SERIALIZER : str
        Object path to serializer function.

    """
    def process_item(self, item, spider):#关键方法
        return deferToThread(self._process_item, item, spider)

    def _process_item(self, item, spider):
        key = self.item_key(item, spider)
        data = self.serialize(item)
        self.server.rpush(key, data)
        return item
```



