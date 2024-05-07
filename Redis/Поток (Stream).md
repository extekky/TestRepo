---
tags:
  - REDIS
---
```python
import redis  
  
r = redis.Redis(host='localhost', port=6379, db=0)  
  
# Добавление сообщений в поток  
r.xadd("mystream", {"key1": "value1", "key2": "value2"})  
  
# Получение сообщений из потока  
messages = r.xrange("mystream", "-", "+")  
for message_id, message in messages:  
    print("Message ID:", message_id.decode(), "Message:", message)
```
