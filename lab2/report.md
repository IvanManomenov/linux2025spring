University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: Администрирование LInux

Year: 2024/2025

Group: K3323

Author: Manomenov Ivan

Lab: Lab2

Date of create: 20.06.25

## 1. Утечка памяти

Была написана прорамма leak.c со следующим кодом:
```
#include <stdlib.h>
#include <unistd.h>

int main() {
    while(1) {
        malloc(1024 * 1024);
        sleep(1);
    }
    return 0;
}

```

Вызываем ее, во втором терминале при помощи команды
```watch -n 1 "ps aux | grep leak | grep -v grep"``` отслеживаем память:

![](https://github.com/IvanManomenov/linux2025spring/blob/main/lab2/lab2-1.png)
![](https://github.com/IvanManomenov/linux2025spring/blob/main/lab2/lab2-2.png)

Как мы видим, память утекает (Резкий рост RSS указывает на утечку)

## 2. Создание зомби-процесса

Был написан скрипт zombie.c:
```
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>

int main() {
    pid_t child_pid = fork();
    if (child_pid == 0) exit(0); 
    else sleep(30);               
    return 0;
}

```

При помощи ```ps aux | grep 'Z'``` детектим зомби-процесс:
![](https://github.com/IvanManomenov/linux2025spring/blob/main/lab2/lab2-3.png)

## 3. CRON

Был создан CRON-процесс
```
*/1 * * * * curl -Is https://github.com/IvanManomenov/linux2025spring/blob/main/lab1/report.md?plain=1 >> /var/log/web_ex.log 2>&1
```
(Каждую минуту заходит на мой отчет по 1 лабе и возвращает логи)
Результат (много логов раз в минуту):
![](https://github.com/IvanManomenov/linux2025spring/blob/main/lab2/lab2-4.png)
