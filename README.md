Disclaimer. Предупреждение.
===========================

PHP interface to JustClick.Ru

This repository created for private puroposes and it's contents is not functional product code.

Этот репозиторий создан для частных нужд и его содержимое не является чем-то функциональным.

Проверка работоспособности
==========================

Создан специальный временный скрип, для проерки как запускается разрабатываемый класс.
```bash
php -q ./justclick2.php
```
Запуск тестов
```bash
phpunit -c app/
phpunit -c app/ src/Acme/StoreBundle/Tests/Controller/
phpunit -c app/ src/Acme/StoreBundle/Tests/Controller/JustClick.php
```
Для сборки проекта и запуска тестов
```bash
ant
```

Работа с Composer
=================

Обновление зависимостей и библиотек
```bash
php composer.phar update
```
Обновление самого запускаемого файла composer.phar
```bash
php composer.phar self-update
```
Добавление новой зависимости
```bash
php composer.phar require guzzlehttp/guzzle:~3
```

Работа с Git
===========

Фиксирование изменений
```bash
git commit -a -m "added travis.yml"
```

Запись изменений на GitHub
```bash
git push https://github.com/bakulev/JustClick.git
```

Планируемые улучшения
=====================

Реализовать повтор вызовов после exception способом, описанным тут:
* http://codehelper.ru/questions/367/springnet-aop-%D0%B7%D0%B0-%D1%81%D1%86%D0%B5%D0%BD%D0%BE%D0%B9-%D1%87%D0%B0%D1%81%D1%82%D1%8C-1
Описание создани Exception в PHP:
* http://project.net.ru/web-master/php/article5/language.exceptions.html

Изменения
========

Сохранение cookie.
------------------

Чтобы сохранять cookie в файл сделал в конструкторе:
```php
$this->client = new Client();
// Установка перманентных cookie в файл.
$cookie_file_name = '/tmp/justclick_cookie.jar';
$cookiePlugin = new CookiePlugin(new FileCookieJar($cookie_file_name));
$this->client->getClient()->getEventDispatcher()->addSubscriber($cookiePlugin);
```
А в 
`vendor/guzzle/plugin-cookie/Guzzle/Plugin/Cookie/CookieJar/ArrayCookieJar.php`
исправил метод 
`function serialize $this->all(null, null, null, false, false)));` 
поставил false, false, чтобы сохранялись не только долгие cookie, но и сессионные.

В класс обработчик файла для cookie
`vendor/guzzle/plugin-cookie/Guzzle/Plugin/Cookie/CookieJar/FileCookieJar.php`
добавил в метод `load` проверку существования и возможности записи в файл.

Работа с Markdown
=================

Хорошее описание работы с `.md` файлами и создание книг на их основе 
* http://habrahabr.ru/post/218433/

Вот тут много полезного синтаксиса использовано
* https://raw.githubusercontent.com/denisshevchenko/ohaskell/master/ru/prepare/create-project.md

Разное
======

Для отладки запросов используется запрос к своему серверу:
```php
$request_url = 'http://tirmethod.vipforex.com/request_debug.php';
```
Описание использования Crawler XPath в Symfony2:
* http://symfony.com/doc/current/components/dom_crawler.html
