# Work-4.1
const http = require('http');

// Беремо порт з першого аргументу командного рядка
const port = process.argv[2];

// Створюємо HTTP-сервер
const server = http.createServer((req, res) => {
  // Перевіряємо, що запит саме GET /
  if (req.method === 'GET' && req.url === '/') {
    res.statusCode = 200;
    res.setHeader('Content-Type', 'text/plain');
    res.end('Welcome to Manual HTTP Router');
  }
});

// Запускаємо сервер на вказаному порту
server.listen(port);

# Work-4.2
const http = require('http');

// Беремо порт з першого аргументу командного рядка
const port = process.argv[2];

// Створюємо HTTP-сервер
const server = http.createServer((req, res) => {
  // Маршрут GET /time
  if (req.method === 'GET' && req.url === '/time') {
    const responseBody = {
      now: new Date().toISOString()
    };

    res.statusCode = 200;
    res.setHeader('Content-Type', 'application/json');
    res.end(JSON.stringify(responseBody));
  }
});

// Запускаємо сервер
server.listen(port);

# Work-4.3
const http = require('http');

// Беремо порт з першого аргументу командного рядка
const port = process.argv[2];

// Створюємо HTTP-сервер
const server = http.createServer((req, res) => {
  // Створюємо URL-об'єкт, щоб зручно читати шлях і query-параметри
  const url = new URL(req.url, `http://localhost:${port}`);

  // Маршрут GET /echo?msg=...
  if (req.method === 'GET' && url.pathname === '/echo') {
    const message = url.searchParams.get('msg') || '';

    res.statusCode = 200;
    res.setHeader('Content-Type', 'text/plain');
    res.end(message);
  }
});

// Запускаємо сервер
server.listen(port);

# Work-4.4
const http = require('http');

// Беремо порт з першого аргументу командного рядка
const port = process.argv[2];

// Створюємо HTTP-сервер
const server = http.createServer((req, res) => {
  // Створюємо URL-об'єкт, щоб читати шлях і query-параметри
  const url = new URL(req.url, `http://localhost:${port}`);

  // Маршрут GET /sum?a=<number>&b=<number>
  if (req.method === 'GET' && url.pathname === '/sum') {
    const a = Number(url.searchParams.get('a'));
    const b = Number(url.searchParams.get('b'));

    // Перевіряємо, чи параметри є числами
    if (Number.isNaN(a) || Number.isNaN(b)) {
      res.statusCode = 400;
      res.setHeader('Content-Type', 'application/json');
      res.end(JSON.stringify({ error: 'Invalid numbers' }));
      return;
    }

    // Якщо все правильно — повертаємо суму
    res.statusCode = 200;
    res.setHeader('Content-Type', 'application/json');
    res.end(JSON.stringify({ sum: a + b }));
  }
});

// Запускаємо сервер
server.listen(port);

# Work-4.5
const http = require('http');

// Беремо порт з першого аргументу командного рядка
const port = process.argv[2];

// Створюємо HTTP-сервер
const server = http.createServer((req, res) => {
  // Для будь-якого невідомого маршруту або методу повертаємо 404
  res.statusCode = 404;
  res.setHeader('Content-Type', 'application/json');
  res.end(JSON.stringify({ error: 'Not found' }));
});

// Запускаємо сервер
server.listen(port);
