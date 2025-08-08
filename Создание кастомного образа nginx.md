## Создание кастомного образа Nginx

### Создание кастомной страницы HTML

    <!DOCTYPE html>

    <html lang="en">
    
    <head>
    
    <meta charset="UTF-8">
    
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <title>Мой Nginx</title>
    
    <style>
    
        body {
        
            font-family: Arial, sans-serif;
            
            text-align: center;
            
            margin-top: 50px;
            
            background-color: #f0f0f0;
            
        }
        
        h1 {
        
            color: #2c3e50;
            
        }
        
    </style>
    
    </head>

    <body>
    
    <h1>Привет, это мой кастомный Nginx!</h1>
    
    <p>Страница загружена из Docker-контейнера на Alpine Linux.</p>
    
    </body>

    </html>

### Создание Docker-файла для сборки образа

#Берём официальный образ Nginx на Alpine

FROM nginx:alpine

#Удаляем стандартную страницу Nginx

RUN rm -rf /usr/share/nginx/html/*

#Копируем нашу страницу в контейнер

COPY index.html /usr/share/nginx/html/

#Открываем порт 80 

EXPOSE 80

#Запускаем Nginx в foreground-режиме 

CMD ["nginx", "-g", "daemon off;"]

### Сборка Docker-образа

docker build -t my-nginx .

docker images

    REPOSITORY    TAG       IMAGE ID       CREATED              SIZE

    my-nginx      latest    fc92f09844c0   About a minute ago   52.5MB

    hello-world   latest    74cc54e27dc4   6 months ago         10.1kB

    (образ собрался)

### Запуск контейнера на порту 8080

docker run -d -p 8080:80 --name my-nginx-container my-nginx

docker ps

