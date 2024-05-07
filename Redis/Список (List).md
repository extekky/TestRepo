---
tags:
  - REDIS
---
```python
import redis  
  
r = redis.Redis(host='localhost', port=6379, db=0)  
  
# Добавление элементов в список  
r.rpush("mylist", "item1")  
r.rpush("mylist", "item2")  
r.rpush("mylist", "item3")  
  
# Получение всех элементов списка  
mylist = r.lrange("mylist", 0, -1)  
for item in mylist:  
    print(item.decode())
```