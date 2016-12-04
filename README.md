Задание:

Существует API, которое умеет отвечать по трём URL: /countries, /cities и /populations. Клиентское приложение подсчитывает численность населения в Африке. Запросы друг от друга не зависят. Чтобы браузер пользователя не простаивал, клиентскому приложению важно уметь делать все три запроса одновременно. Реализацией API является функция getData(url, callback), которая принимает строку с URL запроса и функцию обратного вызова. В случае ошибки в callback первым аргументом будет передана строка ошибки, в случае успеха вторым аргументом будет передан ответ API.
Вам досталась реализация клиентского приложения, которое должно решать описанную выше задачу. Но в коде приложения есть ошибки, из-за которых фактический результат работы отличается от ожидаемого. Сам код здесь.
Как должно быть: приложение выводит в консоль суммарную популяцию в Африке.
Как на самом деле: приложение не выводит в консоль ничего.
Найти ошибку
Исправить
Описать как она могла появиться и почему, как её исправить
Новая функция:
Вывод диалога
Подсчет численности по стране
Подсчет численности по городу


Решение:

Основная ошибка в коде заключается в некорректном определении функции callback внутри цикла for.

В теле цикла for создается внутренняя функция callback изнутри которой происходит обращение 
к переменной request, которая определена области видимости цикла for. При обращении к request - 
callback получит значение на момент обращения. В момент вызова первого callback, цикл for 
уже завершится и request будет иметь последнее значение - '/populations'.

Очевидно, решение заключается в том, чтобы зафиксировать значение request на момент
создания функции callback. 

Для этого была добавлена анонимная функция, которая сохраняет в своей области видимости 
текущее значение request и возвращает функцию обработчик callback, которая в свою очередь
имеет доступ к значению request зафиксированному в области видимости анонимной родительской 
функции.
