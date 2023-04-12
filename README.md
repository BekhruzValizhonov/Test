1) Разница между var, let и const.
 Когда и что лучше использовать?

var item;
console.log(item) // undefined

var можно инициализировать
item = "Hello World"
console.log(item) // Hello World

область видимости, если мы создадим внутри функций переименую то 
она будет видна только в этой функций и вложенных в ней функций

В переименую let можно присвоить новое значение
let num = 10
num = 5

В отличей от var в let нельзя объявить два одинаковых имени в одной области видимости 
let num  = 8
let num  = 10
// Error

В const нельзя присвоить новое значение и нельзя переобъявить 
const y = 3
 y = 6
 // Error

 Если const является объектом то свойство можно изменить. Единственно
 нельзя к const присвоить другой объект.


 На вапрос, когда и что лучше использовать?

 Думаю лучше использовать const, кроме тех случай
 когда вы знаете что переменная будет изменяться,
 используя const вы обозначаете всем что эту переменную изменять не стоит
===============================================
2) Как создать копию объекта, какие способы имеются?

 let obj = {
    val1: "Машина",
    val2: 15
};

let obj2 = Object.assign({},obj);
obj2.val1 = "Велосипед";

console.log(obj.val1); // Машина
console.log(obj2.val2); // 15

Способы: assign(),structuredClone()...
====================================================
3) Как лучше всего выполнить и обработать множество промисов одновременно?

Promise.all() 
Если один из этих Promise равен reject то все промисы будут отклонены

const p1 = Promise.resolve(3);
const p2 = 1337;
const p3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("foo");
  }, 100);
});

Promise.all([p1, p2, p3]).then((values) => {
  console.log(values); // [3, 1337, "foo"]
});

Однако я не думаю что нужно изобретать велосипед для таких операций есть готовые библиотеки   
например один из них: npm i es6-promise-pool
=========================================================
4) Как в Node.js выполнить HTTP запрос к стороннему ресурсу?

const https = require('https');

const options = {
  method: 'GET'
};

let request = https.request('https://jsonplaceholder.typicode.com/users', options, (res) => {
  if (res.statusCode !== 200) {
    res.resume();
    return;
  }

  let data = '';

  res.on('data', (chunk) => {
    data += chunk;
  });

  res.on('close', () => {
    console.log(JSON.parse(data));
  });
});

request.end();

request.on('error', (err) => {
  console.error(err.message);
});
==========================================================
5) Написать функцию, вычисляющую длину последнего слова в строке.

function test(words) {
    let n = words.split(" ");
    return n[n.length - 1];
}
