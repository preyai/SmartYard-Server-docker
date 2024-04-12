# Выбираем базовый образ
FROM node:18-slim

# Установка необходимых инструментов
RUN apt-get update && apt-get install -y \
    lsof \
    net-tools

# Устанавливаем рабочую директорию
WORKDIR /usr/src/app

# Копируем package.json и package-lock.json
COPY ./SmartYard-Server/server/services/push/package*.json ./

# Устанавливаем зависимости
RUN npm install

# Копируем исходный код приложения
COPY ./SmartYard-Server/server/services/push .

# Открываем необходимый порт
EXPOSE 8080

# Запускаем приложение
CMD ["npm", "start"]
