---
tags:
  - REDIS
---
```python
import redis  
  
r = redis.Redis(host='localhost', port=6379, db=0)  
  
# Добавление элементов в множество  
r.sadd("myset", "member1")  
r.sadd("myset", "member2")  
r.sadd("myset", "member3")  
  
# Получение всех элементов множества  
myset = r.smembers("myset")  
for member in myset:  
    print(member.decode())
```