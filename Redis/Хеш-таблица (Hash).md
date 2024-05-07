---
tags:
  - REDIS
---
```python
import redis  
  
r = redis.Redis(host='localhost', port=6379, db=0)  
  
# Установка значения в хеш-таблицу  
r.hset("myhash", "field1", "value1")  
r.hset("myhash", "field2", "value2")  
  
# Получение значения из хеш-таблицы  
value = r.hget("myhash", "field1")  
print(value.decode())  # Выведет: value1
```