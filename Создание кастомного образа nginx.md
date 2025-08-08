## Создание кастомного образа Nginx

Создание кастомной страницы HTML

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

Создание Docker-файла для сборки образа

#Берём официальный образ Nginx на Alpine (лёгкий)
FROM nginx:alpine

#Удаляем стандартную страницу Nginx
RUN rm -rf /usr/share/nginx/html/*

#Копируем нашу страницу в контейнер
COPY index.html /usr/share/nginx/html/

#Открываем порт 80 (Nginx по умолчанию слушает его)
EXPOSE 80

#Запускаем Nginx в foreground-режиме (чтобы контейнер не завершался)
CMD ["nginx", "-g", "daemon off;"]
