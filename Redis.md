１．连接redis（两种方式）

- ```python
    # decode_responses=True: 解决获取的值类型是bytes字节问题
    r = redis.Redis(host='localhost', port='', db=0, decode_responses=True)
  ```

- ```python
    pool = redis.ConnectionPool(host='localhost', port=6379, db=0, decode_responses=True)
    r = redis.Redis(connection_pool=pool)
  ```

２．字符串类型　String

```
  # ex过期时间 单位秒S
  r.set('name', 'Jack', ex=20)
  rst = r.get('name')
  print(rst)   结果：　"Jack"
```

３．列表类型　list　　　　

```python
  r.lpush('object', 'one')
  r.lpush('object', 'two')
  r.lpush('object', 'three')
  r.lpush('object', 'four')
  r.lpush('object', 'five')
  r.lpush('object', 'six')
  ret = r.lrange('object', 0, 5)
  print(ret[::-1], len(ret))   结果：　['one', 'two', 'three', 'four', 'five', 'six'] 　6
```

４．哈希类型  hash

```python
  r.hset('user:info', 'name', 'Jack')
  r.hset('user:info', 'age', 20)
  r.hset('user:info', 'phone', '')
  r.hset('user:info', 'email', '123@gmail.com')
  rst = r.hgetall('user:info')
  print(rst)   结果：　{'age': '', 'email': '123@gmail.com', 'name': 'Jack', 'phone': ''}
```

５．集合类型  set

```python
  r.sadd('set', 'one')
  r.sadd('set', 'two')
  r.sadd('set', 'three')
  res = r.smembers('set')
  print(res)   结果：　{'two', 'one', 'three'}
```

６．有序集合类型　sorted set　

```python
  r.zadd('mark', 'one', 1)
  r.zadd('mark', 'two', 2)
  r.zadd('mark', 'three', 3)
  r.zadd('mark', 'four', 4)
  r.zadd('mark', 'five', 5)
  result = r.zrange('mark', 0, 10)
  print(result)   结果：　['one', 'two', 'three', 'four', 'five']
```

　　