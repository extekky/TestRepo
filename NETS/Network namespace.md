Network namespace - своего рода контейнер для изоляции сетей из хоста. В этом контейнере своя сетевая конфигурация и она не доступна из вне (Но можно это настроить)

Койнейтер может иметь собственные:
- Виртуальные интерфейсы
- Routing tables
- APR tabes
- Свой собственный сетевой интерфейс

Создание нового сетевого интерфейаса:
```bash
sudo ip netns add red
```

```bash
sudp netno is add blue
```

Вывод списка namespaces на хосте:
```bash
ip netns
```

Вывод сетевых интерфейсов в определенном пространстве имен:
```bash
sudo ip netns exec red ip link
```

```bash
sudo ip -n red link
```

Вывод таблиц :
```bash
sudo ip netns exec red arp
```

```bash
sudo ip netns exec red route
```

Создание виртуального кабеля с двумя концами: красный и синий
```bash
sudo ip link add veth-red type veth peer name veth-blue
```

Удаление интерфейса на хосте (сначала нужно его опустить `down`)
```bash
sudo ip link set veth-red down  
sudo ip link delete veth-red
```

Удаление интерфейса в сетевом пространствк имен (сначала опустить `down`)
```bash
sudo ip netns exex red ip link set veth-red down  
sudo ip netns exex red ip link delete veth-red
```
При удалении парного соединения с одного конца, второй коней тоже удалятеся 

Присодение каджого интерфейса к соответсвующему пространству имен
1. Red
   `ip link set veth-red netns red`
2. Blue
   `ip link set veth-blue netns blue`
   
Назначение адресов для каждого из пространств имен
1. Red
   `sudo ip -n red addr add 192.168.15.1/24 dev veth-red`
2. Blue
   `sudo ip -n blue addr add 192.168.15.2/24 dev veth-blue`
   Чтобы узнать адрес:
   `sudo ip netns exec red ip addr show red-violet`
   
Устанавливаем ссылки для возможности взаимодействия
1. Red
   `sudo ip -n red link set veth-red up`
2. Blue
   `sudo ip -n blue link set veth-blue up`
#### Создание сети
Чтобы создать сеть нужен виртуальный коммутатор
Пусть IP коммутатора: `192.168.15.0`

Мы будем использоват технологию `Linux Bridge`

Создадим новый интерфейс на хосте с типом `bridge`
Он будет выступать в роли коммутатора
```bash
sudo ip link add v-net-0 type bridge
```
##### Создание virtual cables для подключения пространств имен к мосту
1. Красный:
   ```bash
   sudo ip link add veth-red type veth peer name veth-red-br
   ```
2. Синий:
   ```bash
   sudo ip link add veth-blue type veth peer name veth-blue-br
   ```
#####  Подключение virtual cables к мосту
###### Красный:
Чтобы подключить один конец интерфейса к простанству имен:
```bash
sudo ip link set veth-red netns red
```

Чтобы подключить другой конец к сети:
```bash
sudo ip link set veth-red-br master v-net-0
```
(master — ведущая сеть для `veth-red-br`)
###### Синий:
Чтобы подключить один конец интерфейса к простанству имен:
```bash
sudo ip link set veth-blue netns blue
```

Чтобы подключить другой конец к сети:
```bash
sudo ip link set veth-blue-br master v-net-0
```
(master — ведущая сеть для `veth-blue-br`)

##### Установка IP адресов для этих линков 
Красный
```bash
sudo ip netns exec red ip addr add 192.168.15.1/24 dev veth-red
```
Синий
```bash
sudo ip netns exec blue ip addr add 192.168.15.2/24 dev veth-blue
```

#####  Запуск интерфейсов
```bash
sudo ip netns exec red ip link set veth-red up
sudo ip netns exec blue ip link set veth-blue up
```

```bash
sudo ip addr add 192.168.15.5/24 dev v-net-0
sudo ip link set v-net-0 up
```