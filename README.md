# set_network_2_device
Настройка сети между двумя устройствами в операционной системе Linux
1. Проверьте доступные сетевые карты
```
ip a
```
2. Выберите нужную карту из вывода, например ```end1```
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: end1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 4a:1c:ea:7a:07:76 brd ff:ff:ff:ff:ff:ff
    inet6 fe80::5d8e:3a77:56d:8533/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever

```
3. Создайте файл настройки сети:
```
sudo nano /etc/netplan/01-network-manager-all.yaml
```
4. Включите в этот файл настроек следующее содержимое
```
network:
  version: 2
  renderer: NetworkManager
  ethernets: 
    end1: # имя вашей сети
      addresses: [192.168.1.2/24] # ваш ip адрес устройства в подсети
      dhcp4: no
      optional: true
```
5. Настройте уровень доступа к файлу
```
sudo chmod 600 /etc/netplan/*.yaml
```
6. Примените изменения для файла настроек
```
sudo netplan apply
```
7. Проверьте пинг сети
```
sudo ping 192.168.1.2
```
