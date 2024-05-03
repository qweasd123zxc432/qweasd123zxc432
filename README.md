// Подключение необходимых модулей
const express = require('express');
const app = express();
const port = 3000;

// Обработка GET запроса на корневой адрес
app.get('/', function(req, res) {
    res.send('Добро пожаловать на мой веб-сайт!');
});

// Обработка GET запроса на адрес /about
app.get('/about', function(req, res) {
    res.send('Страница "О нас"');
});

// Настройка прослушивания порта и запуск сервера
app.listen(port, function() {
    console.log(`Сервер запущен на http://localhost:${port}`);
