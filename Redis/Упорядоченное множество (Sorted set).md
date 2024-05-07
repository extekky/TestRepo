---
tags:
  - REDIS
---
```python
import redis  
  
r = redis.Redis(host='localhost', port=6379, db=0)  
  
# Добавление элементов в упорядоченное множество с указанием оценки (score)  
r.zadd("mysortedset", {"member1": 10, "member2": 20, "member3": 30})  
  
# Получение элементов упорядоченного множества по оценке  
members = r.zrange("mysortedset", 0, -1, withscores=True)  
for member, score in members:  
    print(member.decode(), score)
    
```