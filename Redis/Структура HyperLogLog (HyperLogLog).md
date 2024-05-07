---
tags:
  - REDIS
---
```python
import redis  
  
r = redis.Redis(host='localhost', port=6379, db=0)  
  
# Добавление элементов в HyperLogLog  
r.pfadd("myhyperloglog", "item1", "item2", "item3")  
  
# Получение оценки уникальных элементов  
approx_count = r.pfcount("myhyperloglog")  
print("Approximate Count:", approx_count)
```
