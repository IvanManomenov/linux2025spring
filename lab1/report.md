University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [Администрирование Linux]

Year: 2024/2025

Group: K3323

Author: Manomenov Ivan

Lab: Lab1

Date of create: 13.06.25

### 1. Создать 4 пользователей test1, test2, test3, test4

![](https://github.com/IvanManomenov/linux2025spring/blob/main/lab1/lab1-1.png)

### 2. Для пользователей test1, test2 разрешить получение полномочий root
Для этого добавим их в группу sudo:
```
sudo usermod -aG sudo test1
sudo usermod -aG sudo test2
```

### 3. Для пользователей test3, test4 создать любые файлы в их домашних каталогах
```
sudo -u test3 touch /home/test3/sample_file.txt
sudo -u test4 touch /home/test4/sample_file.txt
```

### 4. Для пользователя test3 разрешить получение полномочий только для выполнения команды tcpdump
Открываем файл sudoers для редактирования:
```
sudo visudo
```
Добавляем следующую строку в файл:
```
test3 ALL=(root) NOPASSWD: /usr/sbin/tcpdump
```

### 5. Создать 2 группы пользователей group1, group2

```
sudo groupadd group1
sudo groupadd group2
```

### 6. Назначить пользователям test2, test3 основную группу group1. Пользователям test1, test4 основную группу group2.
```
sudo usermod -g group1 test2
sudo usermod -g group1 test3
sudo usermod -g group2 test1
sudo usermod -g group2 test4
```

### 7. Для группы group1 разрешить получение полномочий root
Открываем файл sudoers для редактирования:
```
sudo visudo
```
Добавляем следующую строку в файл:
```
%group1 ALL=(ALL:ALL) ALL
```

### 8. Под пользователем test2 создать файл и настроить права доступа
```
sudo -u test2 touch /home/test2/restricted_file.txt
sudo chown test2:group1 /home/test2/restricted_file.txt
sudo chmod 640 /home/test2/restricted_file.txt  # r-w for owner (test2), r for group1, no access for others
```

### 9. Удалить созданные группы и пользователей
![](https://github.com/IvanManomenov/linux2025spring/blob/main/lab1/lab1-2.png)
