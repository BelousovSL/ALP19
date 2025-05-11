# Название выполняемого задания
Научится менять базовые сетевые настройки в Linux-based системах.

# Текст задания
Что нужно сделать?

Соединить офисы в сеть согласно логической схеме и настроить роутинг
Интернет-трафик со всех серверов должен ходить через inetRouter
Все сервера должны видеть друг друга (должен проходить ping)
У всех новых серверов отключить дефолт на NAT (eth0), который vagrant поднимает для связи
Добавить дополнительные сетевые интерфейсы, если потребуется


# Как проверить

Для запуска `vagrant up`


```bash
sergey@fedora:~/Ram/otus-linux$ ssh vagrant@127.0.0.1 -p 2307
vagrant@127.0.0.1's password: 
Welcome to Ubuntu 24.04.2 LTS (GNU/Linux 6.8.0-31-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Sun May 11 02:23:04 PM UTC 2025

  System load:  0.17               Processes:             143
  Usage of /:   14.7% of 30.34GB   Users logged in:       0
  Memory usage: 25%                IPv4 address for eth1: 192.168.1.2
  Swap usage:   0%


This system is built by the Bento project by Chef Software
More information can be found at https://github.com/chef/bento

Use of this system is acceptance of the OS vendor EULA and License Agreements.
Last login: Sun May 11 14:21:11 2025 from 10.0.2.2
vagrant@office2server:~$ traceroute 192.168.2.130
traceroute to 192.168.2.130 (192.168.2.130), 30 hops max, 60 byte packets
 1  _gateway (192.168.1.1)  0.415 ms  0.458 ms  0.450 ms
 2  192.168.255.5 (192.168.255.5)  0.909 ms  0.993 ms  0.986 ms
 3  192.168.255.10 (192.168.255.10)  1.329 ms  1.317 ms  1.307 ms
 4  192.168.2.130 (192.168.2.130)  1.587 ms  1.648 ms  1.640 ms
```

```bash
vagrant@office2server:~$ ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=57 time=45.0 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=57 time=45.9 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=57 time=45.3 ms
^C
--- 8.8.8.8 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 44.956/45.387/45.941/0.411 ms
```

```bash
vagrant@office2server:~$ traceroute 8.8.8.8
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  _gateway (192.168.1.1)  0.255 ms  0.142 ms  0.127 ms
 2  192.168.255.5 (192.168.255.5)  0.390 ms  0.377 ms  0.348 ms
 3  192.168.255.1 (192.168.255.1)  0.486 ms  0.443 ms  0.456 ms
 4  _gateway (10.0.2.2)  0.566 ms  0.537 ms  0.504 ms
 5  * * *
 6  * * *
 7  * * *
 8  morsk-cr02-be21.4024.knd.mts-internet.net (195.34.58.141)  2.155 ms  2.328 ms  2.651 ms
 9  morsk-cr03-ae2.23.knd.mts-internet.net (212.188.54.250)  28.348 ms  26.509 ms  28.278 ms
10  kai-cr02-ae6.23.rnd.mts-internet.net (212.188.0.233)  27.238 ms  26.982 ms  26.800 ms
11  a433-cr06-eth-trunk3.msk.mts-internet.net (212.188.28.133)  26.368 ms  26.990 ms  26.344 ms
12  m9-cr05-ae9.0.msk.mts-internet.net (212.188.28.137)  26.345 ms  26.268 ms  26.206 ms
13  * * *
14  dns.google (8.8.8.8)  38.557 ms  41.753 ms  42.791 ms
```