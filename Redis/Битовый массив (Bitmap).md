---
tags:
  - REDIS
---
```python
import redis  
  
r = redis.Redis(host='localhost', port=6379, db=0)  
  
# Установка бита в битовом массиве  
r.setbit("mybitmap", 0, 1)  
r.setbit("mybitmap", 2, 1)  
  
# Получение значения бита из битового массива  
bit1 = r.getbit("mybitmap", 0)  # Получаем значение бита под индексом 0  
bit2 = r.getbit("mybitmap", 1)  # Получаем значение бита под индексом 1  
  
print(bit1)  # Выведет: True  
print(bit2)  # Выведет: False
```
