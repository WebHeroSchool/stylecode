# stylecod
##### *Здесь собранно 10 правил по стилю кода JavaScript*
---
##### [1. Комментарии](#1)
##### [2. Объявление функций](#2)
##### [3. Объявление переменных](#3)
##### [4. Типы](#4)
##### [5. Строки](#5)
##### [6. Деструктуризация](#6)
##### [7. Классы и конструкторы](#7)
##### [8. Свойства](#8)
##### [9. Свойства](#9)
##### [10. Запятые](#10)


### <a name="1">Комментарии</a>
---
В JavaScript можно использовать два типа комментариев. Первый тип — однострочные комментарии:

``` js
// console.log(foo(5));
```

Они, как следует из названия, располагаются в одной строке. Комментарием считается всё, что идёт за символами //.

>#### Bad
>``` js
>/* console.log(foo(5));*/
>```
>#### Good
>``` js
>// console.log(foo(5));
>```
Второй тип — многострочные комментарии:

>``` js
>/*var foo = function (bar) {
>  return bar++;
>};*/
>```
Тут комментарием считается всё, что находится между комбинацией символов /* и */.

>#### Bad
>``` js
>//var foo = function (bar) {
>  //return bar++;
>//};
>```
>#### Good
>``` js
>/*var foo = function (bar) {
>  return bar++;
>};*/
>```
### <a name="2">Объявление функций</a>
---
Когда JavaScript встречает перенос строки без точки с запятой, он использует правило под названием Автоматическая Вставка Точки с запятой (Automatic Semicolon Insertion), чтобы определить, стоит ли считать этот перенос строки как конец выражения и поместить точку с запятой в вашем коде до переноса строки. 

Однако, ваш код может быть сломан, если JavaScript неверно истолкует ваш перенос строки.

Явное завершение ваших выражений запятыми помогут вам предотвратить возникновение проблем.

>#### Bad
>``` js
>const luke = {}
>const leia = {}
>[luke, leia].forEach((jedi) => jedi.father = 'vader')
>```
>#### Good
>``` js
>const luke = {};
>const leia = {};
>[luke, leia].forEach((jedi) => {
>  jedi.father = 'vader';
>});
>```
### <a name="3">Объявление переменных</a>
---
Используйте const для объявления переменных; избегайте var.

Почему? Это гарантирует, что вы не сможете переопределять значения, т.к. это может привести к ошибкам и к усложнению понимания кода.

>#### Bad
>``` js
>var a = 1;
>var b = 2;
>```
>#### Good
>``` js
>const a = 1;
>const b = 2;
>```
Если вам необходимо переопределять значения, то используйте let вместо var.

Почему? Область видимости let — блок, у var — функция.

>#### Bad
>``` js
>var count = 1;
>if (true) {
>  count += 1;
>}
>```
>#### Good
>``` js
>let count = 1;
>if (true) {
>  count += 1;
>}
>```
Помните, что у let и const блочная область видимости.

>``` js
>// const и let существуют только в том блоке, в котором они определены.
>{
>  let a = 1;
>  const b = 1;
>}
>console.log(a); // ReferenceError
>console.log(b); // ReferenceError
>```
### <a name="4">Типы</a>
---
**Простые типы:** Когда вы взаимодействуете с простым типом, вы напрямую работаете с его значением.

+ `string`
+ `number`
+ `boolean`
+ `null`
+ `undefined`
+ `symbol`

>``` js
>const foo = 1;
>let bar = foo;
>
>bar = 9;
>
>console.log(foo, bar); // => 1, 9
>```
  *Символы не могут быть полностью заполифиллены, поэтому они не должны использоваться, если разработка ведётся для браузеров/сред, которые не поддерживают их нативно.*
**Сложные типы:** Когда вы взаимодействуете со сложным типом, вы работаете со ссылкой на его значение.

+ `object`
+ `array`
+ `function`

>``` js
>const foo = 1;
>let bar = foo;
>
>bar = 9;
>
>console.log(foo, bar); // => 9, 9
>```
### <a name="5">Строки</a>
---
Используйте одинарные кавычки '' для строк.

>#### Bad
>``` js
>const name = "Capt. Janeway";
>```
>#### Good
>``` js
>const name = 'Capt. Janeway';
>```
Строки, у которых в строчке содержится более 100 символов, не пишутся на нескольких строчках с использованием конкатенации.

Почему? Работать с разбитыми строками неудобно и это затрудняет поиск по коду.

>#### Bad
>``` js
>const errorMessage = 'This is a super long error that was thrown because \
>of Batman. When you stop to think about how Batman had anything to do \
>with this, you would get nowhere \
>fast.';
>```
>#### Good
>``` js
>const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
>```
При создании строки программным путём используйте шаблонные строки вместо конкатенации.

Почему? Шаблонные строки дают вам читабельность, лаконичный синтаксис с правильными символами перевода строк и функции интерполяции строки.

>#### Bad
>``` js
>function sayHi(name) {
>  return ['How are you, ', name, '?'].join();
>}
>```
>#### Good
>``` js
>function sayHi(name) {
>  return `How are you, ${name}?`;
>}
>```
Никогда не используйте eval(), т.к. это открывает множество уязвимостей.

Не используйте в строках необязательные экранирующие символы.

Почему? Обратные слеши ухудшают читабельность, поэтому они должны быть только при необходимости.

>#### Bad
>``` js
>const foo = '\'this\' \i\s \"quoted\"';
>```
>#### Good
>``` js
>const foo = '\'this\' is "quoted"';
>const foo = `my name is '${name}'`;
>```
### <a name="6">Деструктуризация</a>
---
При обращении к нескольким свойствам объекта используйте деструктуризацию объекта.

Почему? Деструктуризация избавляет вас от создания временных переменных для этих свойств.

>#### Bad
>``` js
>function getFullName(user) {
>  const firstName = user.firstName;
>  const lastName = user.lastName;
>
>  return `${firstName} ${lastName}`;
>}
>```
>#### Good
>``` js
>function getFullName(user) {
>  const { firstName, lastName } = user;
>  return `${firstName} ${lastName}`;
>}
>```
Используйте деструктуризацию массивов.

>#### Bad
>``` js
>const arr = [1, 2, 3, 4];
>  
>const first = arr[0];
>const second = arr[1];
>```
>#### Good
>``` js
>const arr = [1, 2, 3, 4];
>
>const [first, second] = arr;
>```
Используйте деструктуризацию объекта для множества возвращаемых значений, но не делайте тоже самое с массивами.

Почему? Вы сможете добавить новые свойства через некоторое время или изменить порядок без последствий.

>#### Bad
>``` js
>function processInput(input) {
>  // затем происходит чудо
>  return [left, right, top, bottom];
>}
>
>// при вызове нужно подумать о порядке возвращаемых данных
>const [left, __, top] = processInput(input);
>```
>#### Good
>``` js
>function processInput(input) {
>  // затем происходит чудо
>  return { left, right, top, bottom };
>}
>
>// при вызове выбираем только необходимые данные
>const { left, top } = processInput(input);
>```
### <a name="7">Классы и конструкторы</a>
---
Всегда используйте `class`. Избегайте прямых манипуляций с `prototype`.

Почему? Синтаксис `class` является кратким и понятным.

>#### Bad
>``` js
>function Queue(contents = []) {
>  this.queue = [...contents];
>}
>Queue.prototype.pop = function () {
>  const value = this.queue[0];
>  this.queue.splice(0, 1);
>  return value;
>};
>```
>#### Good
>``` js
>class Queue {
>  constructor(contents = []) {
>    this.queue = [...contents];
>  }
>  pop() {
>    const value = this.queue[0];
>    this.queue.splice(0, 1);
>    return value;
>  }
>}
>```
Используйте extends для наследования.

Почему? Это встроенный способ наследовать функциональность прототипа, не нарушая instanceof.

>#### Bad
>``` js
>const inherits = require('inherits');
>function PeekableQueue(contents) {
>  Queue.apply(this, contents);
>}
>inherits(PeekableQueue, Queue);
>PeekableQueue.prototype.peek = function () {
>  return this.queue[0];
>};
>```
>#### Good
>``` js
>class PeekableQueue extends Queue {
>  peek() {
>    return this.queue[0];
>  }
>}
>```
Методы могут возвращать this, чтобы делать цепочки вызовов.

>#### Bad
>``` js
>Jedi.prototype.jump = function () {
>  this.jumping = true;
>  return true;
>};
>
>Jedi.prototype.setHeight = function (height) {
>  this.height = height;
>};
>
>const luke = new Jedi();
>luke.jump(); // => true
>luke.setHeight(20); // => undefined
>```
>#### Good
>``` js
>class Jedi {
>  jump() {
>    this.jumping = true;
>    return this;
>  }
>
>  setHeight(height) {
>    this.height = height;
>    return this;
>  }
>}
>
>const luke = new Jedi();
>
>luke.jump()
>  .setHeight(20);
>```
Вы можете определить свой собственный метод toString(), просто убедитесь, что он успешно работает и не создаёт никаких побочных эффектов.

>``` js
>class Jedi {
>  constructor(options = {}) {
>    this.name = options.name || 'no name';
>  }
>
>  getName() {
>    return this.name;
>  }
>
>  toString() {
>    return `Jedi - ${this.getName()}`;
>  }
>}
>```
У классов есть конструктор по умолчанию, если он не задан явно. Можно опустить пустой конструктор или конструктор, который только делегирует выполнение родительскому классу.

>#### Bad
>``` js
>class Rey extends Jedi {
>  constructor(...args) {
>    super(...args);
>  }
>}
>```
>#### Good
>``` js
>class Rey extends Jedi {
>  constructor(...args) {
>    super(...args);
>    this.name = 'Rey';
>  }
>}
>```
Избегайте дублирующих членов класса.

Почему? Если объявление члена класса повторяется, без предупреждения будет использовано последнее. Наличие дубликатов скорее всего приведёт к ошибке.

>#### Bad
>``` js
>class Foo {
>  bar() { return 1; }
>  bar() { return 2; }
>}
>```
>#### Good
>``` js
>class Foo {
>  bar() { return 1; }
>}
>```
Метод класса должен использовать this или быть преобразованным в статический метод.

>#### Bad
>``` js
>class Foo {
>  bar() {
>    console.log('bar');
>  }
>}
>```
>#### Good
>``` js
>// используется this
>class Foo {
>  bar() {
>    console.log(this.bar);
>  }
>}
>// конструктор освобождается
>class Foo {
>  constructor() {
>    // ...
>  }
>}
>// статические методы не должны использовать this
>class Foo {
>  static bar() {
>    console.log('bar');
>  }
>}
>```
### <a name="8">Свойства</a>
---
Используйте точечную нотацию для доступа к свойствам.

>#### Bad
>``` js
>const luke = {
>  jedi: true,
>  age: 28,
>};
>
>const isJedi = luke['jedi'];
>```
>#### Good
>``` js
>const luke = {
>  jedi: true,
>  age: 28,
>};
>
>const isJedi = luke.jedi;
>```
Используйте скобочную нотацию [ ], когда название свойства хранится в переменной.

>``` js
>const luke = {
>  jedi: true,
>  age: 28,
>};
>
>function getProp(prop) {
>  return luke[prop];
>}
>
>const isJedi = getProp('jedi');
>```
Используйте оператор ** для возведения в степень.

>#### Bad
>``` js
>const binary = Math.pow(2, 10);
>```
>#### Good
>``` js
>const binary = 2 ** 10;
>```

### <a name="9">Блоки</a>
---
Используйте фигурные скобки, когда блок кода занимает несколько строк.

>#### Bad
>``` js
>function foo() { return false; }
>```
>#### Good
>``` js
>function bar() {
>  return false;
>}
>```
Если блоки кода в условии if и else занимают несколько строк, расположите оператор else на той же строчке, где находится закрывающая фигурная скобка блока if.

>#### Bad
>``` js
>if (test) {
>  thing1();
>  thing2();
>}
>else {
>  thing3();
>}
>```
>#### Good
>``` js
>if (test) {
>  thing1();
>  thing2();
>} else {
>  thing3();
>}
>```

### <a name="10">Запятые</a>
---
Не начинайте строку с запятой.

>#### Bad
>``` js
>const story = [
>    once
>  , upon
>  , aTime
>];
>```
>#### Good
>``` js
>const story = [
>  once,
>  upon,
>  aTime,
>];
>```
Добавляйте висячие запятые.

Почему? Такой подход даёт понятную разницу при просмотре изменений. Кроме того, транспиляторы типа Babel удалят висячие запятые из собранного кода, поэтому вы можете не беспокоиться о проблемах в старых браузерах.

>#### Bad
>``` js
>const hero = {
>     firstName: 'Florence',
>-    lastName: 'Nightingale'
>+    lastName: 'Nightingale',
>+    inventorOf: ['coxcomb chart', 'modern nursing']
>};
>```
>#### Good
>``` js
>const hero = {
>     firstName: 'Florence',
>     lastName: 'Nightingale',
>+    inventorOf: ['coxcomb chart', 'modern nursing'],
>};
>```