University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [Администрирование Linux]

Year: 2024/2025

Group: K3323

Author: Manomenov Ivan

Lab: Lab3

Date of create: 21.06.25

### 1. Создание FastAPI 

Был создан файл main.py:

```
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
async def root():
    return {"message": "Hello World"}
```

### 2. Создание DockerFile

Создадим DockerFile

```
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY ./main.py .

EXPOSE 8000

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

### 3. Построение Docker-образа

![](https://github.com/IvanManomenov/linux2025spring/blob/main/lab3/lab3-1.png)

### 4. Проверка
Запускаем на http://localhost:8000/

![](https://github.com/IvanManomenov/linux2025spring/blob/main/lab3/lab3-2.png)

Успех
