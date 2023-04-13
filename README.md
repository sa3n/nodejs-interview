# NodeJS Interview Questions

Материалы взяты из различных источников

## Общие вопросы

1. Какие парадигмы программирования поддерживает JavaScript?
2. Функциональное программирование. Плюсы и минусы
3. ООП. Плюсы и минусы
4. Что такое TDZ (Temporal Dead Zone)?
5. Чем отличаются необъявленная переменная от переменных, содержащих `null` или `undefined`?
6. Как определяется значение `this`?
7. Что такое hoisting (поднятие)?
8. Разница между `var`, `let`, `const`?
9. Область видимости функций и блочная область видимости
10. 'use strict'
11. `0.3 – (0.2 + 0.1)` вернёт очень маленькую дробь. Как проверить, что 0.3 равно 0.2 + 0.1?
12. Что выведет следующий код?

```
const length = 10;

function fn() {
	console.log(this.length);
}

const obj = {
    length: 5,
    method: function(fn) {
        fn();
        arguments[0]();
    }
};

obj.method(fn, 1);
```

13. `const a = [1, 2, 3]`. Что произойдёт при `a[10] = 99`? Что выведет `console.log(a[6])`?
14. Поднятие (hoisting)?
15. AJAX
16. Что выведет следующий код?

```
(function(){
  var a = b = 3;
})();
```

17. Типы ошибок в JavaScript
18. Чем отличается лексическая область видимости от динамической?
19. Обработка исключений
20. Оператор `!!`
21. Разница между spread- и rest-операторами
22. Проверка чётности числа без оператора `%`
23. Проверка существования подстроки в строке
24. Как проверить, является ли число конечным?
25. Чем отличается `isNaN()` от `Number.isNaN()`?
26. Garbage collector
27. Как обработать неперехваченные исключения в Node?
28. NODE_ENV
29. globals

## Algorithms

1. QuickSort
2. MergeSort
3. DFS
4. BFS

## Architecture

1. Какие плюсы и минусы у монолитной и микросервисной архитектур?

## API

* REST
* GraphQL
* RPC
* gRPC
* SOAP
* HATEOAS
* XML-RPC
* GSON
* BPEL
* BPM
* ESB

## Async/await

1. Сравните использование async/await и генераторов

## Authentication

1. Token-based authentication
2. JWT
3. OAuth

## Buffer

1. ArrayBuffer
2. TypedArrays
3. DataView

## Child Processes/Threads

1. Методы `.fork()` и `.spawn()`
2. Разница между child process и worker threads
3. node:process
4. node:cluster
5. SharedArrayBuffer

## Collections

1. В чём разница между массивом и объектом?
2. Методы массивов `.forEach()` и `.map()`
3. В чём разница между объектами `Map` и `WeakMap`?
4. Как проверить, является ли объект массивом?
5. Какие конструкции языка используются для обхода массивов и объектов
6. Как добавить элемент в начало массива?
7. Как проверить, является ли объект массивом?
8. Как добавить элемент в начало массива?
9. `const a = [1, 2, 3]`. Выбросит ли ошибку `a[10] = 99`? Что выведет `console.log(a[6])`?
10. Как удалить дубликаты из массива?
11. Почему доступ к элементу массива производится за O(1)?
12. Как найти потерянное целое число в массиве с числами от 1 до 100?
13. Как объединить два сортированных массива в один сортированный?
14. Сравнение массивов
15. Как отсортировать массив нулей и единиц?
16. Дан массив и целевая сумма двух элементов. Как найти индексы элементов, которые дают такую сумму?
17. В чем разница между `Set` и `WeakSet`?
18. `Map`
19. `Set`
20. `WeakMap`
21. `WeakSet`

## Data Types/Formats

1. Как можно написать собственную функцию `isInteger(x)`
2. Что такое `NaN`? Какой у `NaN` тип? Как проверить на `NaN`?
3. Как проверить null?
4. Что такое ступенчатый (зубчатый, jagged) массив?
5. В чём разница между примтивными типами и объектными типами?
6. JSON
7. Мутабельные и иммутабельные типы данных
8. Boxing/unboxing в JavaScript
9. Почему не стоит использовать конструкторы типа new String?
10. Записи (records) и кортежи (tuples)
11. Почему `typeof null` возвращает `object`?
12. Как происходит преобразование типов в следующих примерах:

```
    {}+[]+{}+[1]
    !!"false" == !!"true"
    ['x'] == 'x'
```

13. Symbol

## Data Structures

1. Linked List
2. Stack
3. Queue
4. Binary Tree
5. BST
6. Heap
7. Priority Queue

## Databases

1. Чем отличается embed- от reference-связи в MongoDB?
2. ActiveRecord и DataMapper
3. Транзакции
4. ACID
5. n + 1
6. MongoDB Aggregation Pipeline

## EventLoop/Node.js Architecture

<details>
    <summary>1. EventLoop (Цикл событий)</summary>
    В браузере:

    * Call Stack. Часть движка JS (V8)
    * Task Queue. Часть EventLoop. На самом деле две очереди FIFO:
        * Macrotask Queue (aka Event Queue)
        * Microtask Queue (aka Task Queue, aka Promise Jobs).
    * Web APIs
        * отвечает за регистрацию событий, таймаутов и ... ?

    За что отвечает движок (V8):
    * Heap — место аллокации памяти для всех переменных, объявленных в программе (код функций, например, тоже аллоцируется в памяти)
    * Call Stack — стек, в который добавляются функции, выполняются одна за другой и удаляются, когда выполнение завершено
    * malloc, garbage collector
    * компиляция в машинный код
    * оптимизации

    EventLoop не является частья движков. EventLoop предоставляется средой (NodeJS, браузер, ...)

    Микрозадачи:
    * Promise (99% случаев)
    * queueMicrotask — явное создание микрозадач
    * mutationObserver (только браузер, часть WebAPI)

    Макрозадачи:
    * Таймеры
    * События
    * I/O
    * ....

    * Задачи из Task Queue попадают в Call Stack только после того как Call Stack очистится.
    * В приоритет всегда микрозадачи. Разом выполняются ВСЕ микрозадачи, а потом ОДНА макрзадача (так как макрозадача может породить микрозадачу)

    Три фазы EventLoop:
    1. Call Stack (пока не опустеет)
    2. Microtask Queue (все задачи)
    3. Macrotask Queue (одна задача)

    ---

    В NodeJS:

    Задача NodeJS — преобразовать код JS в машинный код.

    Составные части:
    * Движок V8
    * libuv
        * кроссплатформенный I/O
            * работа с файлами
            * работа с сетью
        * EventLoop

    Libuv управляет пулом потоков Thread Pool (по-умолчанию четырьмя)

    Думультиплексор событий — механизм ОС для организации неблокирующего ввода/вывода (epoll, IOCP, kqueue в Linux, Windows, MacOS, соответственно)

    Фазы EventLoop:
    0. не указано в доке — Promise
    1. Timers (таймеры): setTimeout, setInterval 
    2. I/O-callbacks: все обратные вызовы, кроме setTimeout, setInterval, setImmediate и событий 'close'. В том числе on. 'error'. Название очереди — Callback Queue
    3. Idle/Prepare (ожидание/подготовка) — только для внутренних нужд (пример: составить отчёт о производительности в момент простоя приложения). У программиста нет никакого доступа
    4. Poll (опрос) — получение новых событий ввода-вывода. Здесь Нода может блокироваться, если необходимо. Когда завершается выполняемая в фоновом режиме операция, ядро ОС сообщает Ноде, что функция обратного вызова этой операции может быть добавлена в Poll Queue (название очереди). В основном I/O-операции чтения файлов? По сути — опрос событий, который будут выполнены в следующей (?) итерации? setImmediate
    5. Check (проверка) — обратные вызовы setImmediate
    6. Close Callbacks — обратные вызовы .on 'close'

    * Каждая фаза имеет FIFO-очередь обратных вызовов. Итого 6 очередей! В официальной доке в псевдокоде описаны три:
        * pendingTimers (setTimeout, setInterval)
        * pendingOSTasks (сервер, слушающий порт, например)
        * pendingOperations (долгие операции, например чтение файловой системы)
    * Когда EventLoop входит в конкретную фазу, он запускает функции обратного вызова из очереди этой фазы до тех пор, пока очередь не опустеет!
    * Когда очередь очередной фазы опустеет, EventLoop переходит к следующей фазе
    * Коллбэки process.nextTick() срабатывают в ту же фазу, где были вызваны (считай — между фазами)

    Приоритетные очереди (исполняются, когда EventLoop не находится ни в одной из перечисленных фаз):
    * nextTickQueue
    * Microtask Queue

</details>

2. В чём разница между стеком вызовов и очередью задач?
3. Микрозадачи и макрозадачи
4. Преимущества однопоточной модели Node.js
5. Разница между `process.nextTick` и `setImmediate`?
6. Thread pool
7. V8
8. Почему при рекурсивном вызове `nextTick` блокирует цикл событий, а `setImmeidate` — нет?
9. Паттерн Reactor и Node.js

## EventEmitter

7. EventEmitter

## Functions

1. Первоклассные функции
2. Разница между `.call()`, `.apply()` и `.bind()`
3. Зачем использовать IIFE?
4. Когда следует использовать стрелочные функции?
5. Для чего обычно используются анонимные функции?
6. Генераторы
7. Когда стоит использовать генераторы?
8. Что такое замыкание? Приведите примеры
9. Почему запись `function foo(){}()` не работает как IIFE?
7. Объясните разницу между `person = Person()` и `person = new Person()`
8. Что выведет следующий код?

```
(function(){
    var a = b = 3;
})();

console.log(typeof a !== 'undefined');
console.log(typeof b !== 'undefined');
```

9. Зачем заключать всё содержимое JS-файла в блок функции?
10. Напишите функцию sum, которая будет работать корректно как `sum(2, 3)`, так и `sum(2)(3)`
11. Что такое замыкания? Приведите примеры
12. Почему запись `function foo(){}()` не работает как IIFE?
13. Обход массивов
14. Что выведет следующий код?

```
const length = 10;

function fn() {
	console.log(this.length);
}

const obj = {
    length: 5,
    method: function(fn) {
        fn();
        arguments[0]();
    }
};

obj.method(fn, 1);
```

15. Как работает метод `.reduce()`?
16. this в обычной и стрелочной функциях
17. Функции высшего порядка
18. Как бы вы реализовали метод `Array.prototype.map`?
19. Как бы вы реализовали метод `Array.prototype.filter`?
20. Как бы вы реализовали метод `Array.prototype.reduce`?
21. Объект arguments
22. Как бы вы реализовали вспомогательную функцию мемоизации?
23. Как узнать, сколько аргументов ожидает получить функция?
24. Работа с датами в JS
25. Каррирование
26. Частичное применение
27. Что выведет следующий код?

```
let f = function() {
    console.log(1);
}

const execute = function(f) {
    setTimeout(f, 1000);
}

execute(f);

f = function() {
    console.log(2);
}
```

28. Потеря контекста
29. Итераторы
30. Приведите примеры использования мемоизации
31. Функции обратного вызова (callbacks)
32. Позднее связывание

## HTTP

1. Версии протокола HTTP
2. Коды ответа (состояние) HTTP
3. Ограничения встроенного модуля http в Node.js?
4. Типы HTTP-запросов
5. В чём разница между HTTP-методами PUT, POST, UPDATE?
6. TCP и HTTP
7. HTTPS

## Modules. Packages

1. CommonJS
2. ES2015
3. Паттерны импортирования модулей
4. package-lock.json
5. Разница между `npm install` и `npm ci`
6. Плюсы yarn по сравнению с npm?
7. Локальная и глобальная установкой npm-пакетов
8. DI

## Objects

1. В чём разница между `Object.freeze()` и ключевым словом `const`?
2. Как организовать глубокую заморозку объекта?
3. Как сделать копию объект? Глубокая (deep) копия и поверхностная (shallow)
4. Почему не следует использовать `x === 'object'` для проверки того, что x — объект?
5. Что выведет следующий код?

```
let a = {}
let b = { key: 'b' }
let c = { key: 'c' }

a[b]=123
a[c]=456

console.log(a[b]);
```
6. Способы клоинрования объектов
7. Объясните разницу между `const person = Person()` и `const person = new Person()`
8. В чём проблема с `typeof bar === 'object` для проверки того, что bar — объект? Как её избежать?
9. Что выведет следующий код?

```
const a = {},
const b = {key:'b'},
cinst c = {key:'c'};
a[b] = 123;
a[c] = 456;
console.log(a[b]);
```

10. Что выведет следующий код?

```
const obj = {}
console.log(obj.someprop.x)
```

11. Проверка наличия свойства в объекте
12. Разница между `Object.freeze()` и `Object.seal()`
13. Как проверить, что объект является пустым?
14. Разница между `===` и `Object.is()`
15. Что такое аксессоры?
16. DMZ-объекты
17. Деструктуризация объектов
18. Способы копирования простого объекта типа `obj = { a: 1, b: 2, c: 3 }`
19. Функция structuredClone()
20. Дескрипторы свойств объектов
21. Создание неизменяемых объектов

## OOP. Classes

1. Классическое наследование и прототипное наследование
2. Разница между ES6-классами и конструкторами функций
3. Классы в JS
4. Статические классы
5. Абстрактные классы
6. Инкапсуляция. Приёмы в JS
6. Полиморфизм. Приёмы в JS
7. Разница между композицией и наследованием
8. SOLID

## Patterns

1. Открытый модуль (Revealing Module)
2. Middleware
3. Observer
4. Pub/sub
5. CQS
6. CQRS
7. Event Sourcing
8. GRASP

## Promises

1. PromiseAPI
2. Преимущества и недостатки использования PromiseAPI вместо обратных вызовов
3. Чем отличается Promise от Observable?
4. Что выведет следующий код?

```
Promise
    .resolve(10)					
    .then(e => console.log(e))
    .then(e => Promise.resolve(e))
    .then(console.log)
    .then(e => {
        if (!e) {
            throw 'Error caught'
        }
    })
    .catch(e => {
        console.log(e)
        return new Error('New error')
    })
    .then(e => {
        console.log(e.message)
    })
    .catch(e => {
        console.log(e.message)
    });
```

5. Разница между `Promise.all()` и `Promise.allSettled()`

## Protocols/Network

1. node:net
2. WebSockets

## Prototypes

1. В чём заключается разница между классическим наследование и прототипным наследованием?
2. Когда прототипное наследование является хорошим выбором?
3. В чём разница между `__proto__` и `prototype`?
4. Можно ли записывать новые свойства/методы в прототипы стандартных классов и в каких случаях? Как обезопасить себя, если нужно расширить прототип? 

## Proxy API/ Reflect API

1. Proxy API
2. Приведите примеры использования Proxy API
3. Reflect API


## RegExp

1. Разница между методами `test()` и `exec()`?
2. Методы для работы с регулярными выражениями в JS

## Security

1. XSS
2. Как происходит проверка правильности пароля при использовании bcrypt?
3. CORS
4. Заголовки CORS

## Standards

1. ECMAScript

## Streams

1. Streams
2. Разница между `readFile` и `createReadStream`?

## SQL

<details>
    <summary>1. Нормальные формы 1NF, 2NF, 3NF</summary>

    Нормализация — организация данных в БД путём установления отношений между ними, устранения избыточности и несогласованных зависимостей.

    Существуют правила нормализации. Каждое правило называют нормальной формой (NF). Если выполняется первое правило, говорят, что БД в 1NF, если первые три — в 3NF, и т. д.

    Денормализованная база данных содержит большое количество избыточных данных, требуется меньше join'ов во время запросов. В нормализованной — наоборот (меньше избыточности, больше join'ов).

    Пример таблицы без нормализации:

    | Name        | Address             | Movies                                          |
    |-------------|---------------------|-------------------------------------------------|
    | Janet Jones | First Street Plot 4 | Pirates of the Caribbean, Clash of Titans       |
    | Robert Phil | 3rd Street 34       | Forgetting Sarrah Marshal, Daddy's Little Girls |
    | Robert Phil | 5th Avenue          | Clash of Titans                                 |

    1NF:
    * Устранены повторяющиеся группы в отдельных таблицах (например столбцы Movie1, Movie2, Movie3) или массивы (каждая ячейка таблицы должна содержать одно значение)
    
    Пример таблицы в 1NF:

    | Name        | Address             | Movie                     |
    |-------------|---------------------|---------------------------|
    | Janet Jones | First Street Plot 4 | Pirates of the Caribbean  |
    | Janet Jones | First Street Plot 4 | Clash of Titans           |
    | Robert Phil | 3rd Street 34       | Forgetting Sarrah Marshal |
    | Robert Phil | 3rd Street 34       | Daddy's Little Girls      |
    | Robert Phil | 5th Avenue          | Clash of Titans           |

    2NF:
    * Таблицы должны быть в 1NF
    * Устранена избыточность (созданы таблицы для наборов значений, относящихся к нескольким записям, а сами таблицы связаны внешними ключами)

    Пример БД в 2NF:

    | Id | Name        | Address             |
    |----|-------------|---------------------|
    | 1  | Janet Jones | First Street Plot 4 |
    | 2  | Robert Phil | 3rd Street 34       |
    | 3  | Robert Phil | 5th Avenue          |

    | Movie                     | Person Id |
    |---------------------------|-----------|
    | Pirates of the Caribbean  | 1         |
    | Clash of Titans           | 1         |
    | Forgetting Sarrah Marshal | 2         |
    | Daddy's Little Girls      | 2         |
    | Clash of Titans           | 3         |

    3NF:
    * Таблицы должны быть в 2NF
    * Все неключевые поля, содержимое которых может относиться к нескольким записям выносятся в отдельные таблицы

    Cсылки:
    * https://learn.microsoft.com/ru-ru/office/troubleshoot/access/database-normalization-description

</details>

2. `LEFT JOIN`
3. `INNER JOIN`
4. `FULL OUTER JOIN`
5. Напишите SQL-запрос, который выбирает трех авторов, у которых больше всего книг
6. Напишите SQL-запрос, который выбирает последние три комментария для конкретного пользователя для двух таблиц: comments и authors
7. Оператор HAVING
8. `GROUP` BY, аггрегация
9. Напишите SQL-запрос, который выбирает последние три комментария для каждого пользователя для двух таблиц: comments и authors
10. Типы данных MySQL
11. `INSERT`
12. `CREATE TABLE`
13. Constraints
14. `ALTER`
15. Разница между `CHAR` и `VARCHAR`
16. Разница между `DECIMAL`, `FLOAT`, `DOUBLE`
17. `CREATE FUNCTION`
18. `CREATE PROCEDURE`

## Testing

1. Пирамида тестирования
2. Unit-тесты
3. Code-coverage
4. Что такое стабы (stubs)?

## Timers

1. Таймеры в JavaScript
2. Что выведут следующие фрагменты кода:

```
for (let i = 0; i < 5; i++) {
	setTimeout(function() { 
        console.log(i) 
    }, i * 1000 )
}  

for (var i = 0; i < 5; i++) {
	setTimeout(function() { 
        console.log(i) 
    }, i * 1000 )
} 
```

3. `setImmediate`
4. Разница между `setImmediate` и `setTimeout(0)`?

## TypeScript

1. Объявление функций
2. Полиморфизм
3. Интерфейсы
4. Generics

## Version Control

1. Системы контроля версий
2. `git fetch`
3. Git-hygiene подходы
4. Разница между `git merge` и `git rebase`
5. Staging area
6. `git reset --hard`
7. `git merge`
8. `git checkout`
9. `git rebase`
10. `git stash`
11. `git revert`

## Web APIs

1. localStorage, sessionStorage, cookies

<!-- <details>
  <summary>Вопрос</summary>
  Ответ
</details> -->