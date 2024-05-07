---
tags:
  - REDIS
---
```python
import redis  # Импорт основной библиотеки  
import json  # Для красивого вывода  
  
bd = redis.Redis(host='localhost', port=6379, db=0)  # Подключение к базе данных  
  
# Задаем значения для хэш таблицы (hset) в формате (<name_hash> <field> <value>)  
bd.hset("user:id:100", "username", "john")  
bd.hset("user:id:100", "email", "john@example.com")  
  
# Добавляем элементы в список (list) в формате (<name list> <value>)  
bd.rpush("mylist", "item1")  
bd.rpush("mylist", "item2")  
  
# Устанавливаем значения типа string в формате (<name> <value>)  
bd.set("number", "10")  
bd.set("str", "Hello, World!")  
  
# Удаление всех переменных (очистка базы данных redis) for i in bd.keys('*'):  
    bd.delete(i)  
  
# Вывод всех типов данных  
for i in bd.keys('*'):  
    if bd.type(i) == b'hash':  
        print('TYPE: hash', end='\n')  
        print(  
            json.dumps(  
                {  
                    key.decode(): value.decode() for key, value in bd.hgetall(i).items()  
                }, indent=4  
            )  
        )  
    elif bd.type(i) == b'string':  
        print('TYPE: string', end='\n')  
        print(  
            json.dumps(  
                {  
                    "NAME: ": i.decode(),  
                    "VALUE: ": bd.get(i).decode()  
                }, indent=4  
            )  
        )  
    elif bd.type(i) == b'list':  
        print('TYPE: list', end='\n')  
        print(  
            json.dumps(  
                [  
                    value.decode() for value in bd.lrange(i, 0, -1)  
                ], indent=4  
            )  
        )  
    else:  
        print('TYPE: unknown', end='\n')  
        print(  
            json.dumps(  
                {  
                    bd.get(i).decode()  
                }, indent=4  
            )  
        )
```