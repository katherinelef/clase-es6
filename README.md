## Template string

```js
const cl = console.log;

let specie = 'dog';
let sound = 'woof';

cl(`The ${specie} says ${sound}`);
```

## Arreglos

la propiedad `.length`

sirve tanto para consultar, como para modificar el arreglo.

```js
let arr = [ 'a', 'b', 'c' ];
arr.length; // cantidad de elementos
// 3
arr.length = 2; // elimina el último elemento
arr;
// [ 'a', 'b' ]
arr[arr.length] = 'd'; // agrega un elemento al final
arr;
// [ 'a', 'b', 'd' ]

// copiar un array
let arrV2 = arr.slice();
```

```js
let arr = [1, 2, 3, 4, true, 'true', 5, 6];

console.log(arr.length);
// 8
console.log(arr[5]);
// true

let sum = 0;

for (let index = 0; index < arr.length; index++) {
  let element = arr[index];

  if (typeof element === 'number') {
    sum += element;
  }
}

for (let index = 0; index < arr.length; index++) {
  let element = arr[index];

  if (typeof element !== 'number') continue;
  
  sum += element;
}
console.log(sum);
// 21
```

### Prototipo, molde o clase

```js
let arr = ['a', 'b', 'c'];

console.log(arr.saludo);
// undefined

Array.prototype.saludo = 'Hola mundo!!!';
console.log(arr.saludo);
// Hola mundo!!!
```

## Métodos varios

`push()`, `pop()`, `shift()`, `unshift()`, `includes()`, `forEach()`, `indexOf()`, `lastIndexOf()`, `join()`, `reverse()`, `splice()`, `slice()`, `toString()`, `find()`, `findIndex()`, `sort()`, `etc...`

```js
let arr = [1, 2, 3, 4];
let cl = console.log;

cl(arr.push(6));
// 5
cl(arr.unshift(-1));
// 6
cl(arr.pop());
// 6
cl(arr.shift());
// -1

cl(arr.includes(1));
// true
cl(arr.includes(4));
// true
cl(arr.includes(100));
// false

arr.forEach(function(element) { cl(element) });
// 1
// 2
// 3
// 4

cl(arr.indexOf(4));
// 3

arr.push(2, 3);
// [1, 2, 3, 4, 2, 3]
cl(arr.lastIndexOf(2));
// 4

cl(arr.join());
// "1,2,3,4,2,3"
cl(arr.join('\n'));
// "1
//  2
//  3
//  4
//  2
//  3"

cl(arr.reverse());
// [3, 2, 4, 3, 2, 1]

// elimina o aniade elementos, .splice(desde, cantidad, items)
cl(arr.splice(4, 5));
// [2, 1]
cl(arr);
// [3, 2, 4, 3]

arr = [1, 2, 3, 4];

cl(arr.splice(0));
// [1, 2, 3, 4]
cl(arr);
// []

arr = [1, 2, 3, 4];

cl(arr.splice(2));
// [3, 4]

cl(arr.splice(2, 0, ...[3, 4]));
// [1, 2, 3, 4]

arr = [1, 2, 3, 4];

cl(arr.slice(1));
// [2, 3, 4]
cl(arr.slice(1, 3));
// [2, 3]

// genera una copia
let copiaArr = arr.slice();
cl(copiaArr);
// [1, 2, 3, 4]

cl(arr.toString());
// "1,2,3,4"

cl(arr.find((element) => element > 3));
// 4
cl(arr.findIndex((element) => element > 3));
// 3

arr.push(-1, -2, -3, 0);
cl(arr);
// [1, 2, 3, 4, -1, -2, -3, 0]
cl(arr.sort());
// [-3, -2, -1, 0, 1, 2, 3, 4]

```
## Iteradores

Son objetos que contienen el método `.next()`, este método devuelve 2 propiedades: `value y done`.

`.keys()` y `.entries()`.

```js
let arr = [1, 2, 'a', 'b'];

let iterador = arr.keys();

console.log(iterador.next());
// {value: 0, done: false}
console.log(iterador.next());
// {value: 1, done: false}
console.log(iterador.next());
// {value: 2, done: false}
console.log(iterador.next());
// {value: 3, done: false}
console.log(iterador.next());
// {value: undefined, done: true}

let iterador = arr.entries();

console.log(iterador.next());
// {value: [0, 1], done: false}
console.log(iterador.next());
// {value: [0, 2], done: false}
console.log(iterador.next());
// {value: [0, 'a'], done: false}
console.log(iterador.next());
// {value: [0, 'b'], done: false}
console.log(iterador.next());
// {value: undefined, done: true}
```

## Algunos métodos importantes de ES6

`.map()`, `.filter()` y `.reduce()`

```js
let estudiantes = [
  {
    nombre: 'Alejandra',
    calificacion: 20
  },
  {
    nombre: 'Ruth',
    calificacion: 18
  },
  {
    nombre: 'Michelle',
    calificacion: 16
  },
  {
    nombre: 'Mariana',
    calificacion: 14
  },
  {
    nombre: 'Gabriela',
    calificacion: 12
  },
];

let nombreEstudiantes = estudiantes.map((estudiante) => estudiante.nombre);

let estudiantesAprobados = estudiantes.filter((estudiante) => estudiante.calificacion >= 10);

// primero un corto ejemplo con reduce
let numeros = [2, 4, 6, 8, 10];
let suma = numeros.reduce((a, b) => a + b);
console.log(suma);
// 30
let mayor = numeros.reduce((a, b) => a > b ? a : b);
console.log(mayor);
// 10

let promedio = numeros.reduce((a, b, i, numeros) => {
  b += a;
  let promedio;

  if (i === numeros.length - 1)
    promedio = b / numeros.length;
  else
    promedio = b;
  return promedio;
});

let promedioNotas = estudiantes.reduce((a, b, i, estudiantes) => {
  let objPromedio;

  if (i < estudiantes.length - 1)
    objPromedio = { calificacion: a.calificacion += b.calificacion };
  else
    objPromedio = (a.calificacion + b.calificacion) / estudiantes.length;
  
  return objPromedio;
});

// mejorando el código
let promedioNotas = estudiantes.reduce((a, b, i, estudiantes) => {
  let objPromedio;
  
  b.calificacion += a.calificacion;

  if (i === estudiantes.length - 1)
    objPromedio = b.calificacion / estudiantes.length;
  else
    objPromedio = { calificacion: b.calificacion };
  
  return objPromedio;
});
```

## Objetos

```js
const LAB = {
  nombre: 'laboratoria',
  sedes: ['Ciudad de México', 'Lima', 'Santiago de Chile'],
  profes: {
    SCL: {
      seniors: {
        'front-end': ['Fabián', 'Alexandra', 'Belé'],
        'UX': ['Claire']
      },
      juniors: ['Allison', 'Marcia', 'Nadia']
    },
    CDMX: {
      seniors: {
        'front-end': ['Manu'],
        'UX': ['Camilo']
      },
      juniors: ["Amalia", "Silvana", "Karla", "Jonh"]
    },
    LIMA: {
      seniors: {
        'front-end': ['Joalbert'],
        'UX': ['Gonzalo']
      },
      juniors: ['Ruth', 'Michelle', 'Gabriela', 'Lulu']
    }
  },
  mejorStartupSocial: true,
  fundacion: 2014,
  eslogan: 'código que transforma',
  // esto no es ES6
  saludo: function() { return 'Bienvenidxs a Laboratoria' }
};

console.log(LAB.saludo());

try {
    console.log(LAB.despedida());
} catch(e) {
    console.log(`error: ${e}`);
} finally {
    console.log('Con error o sin error siempre me imprimo!!!');
}
// Bienvenidxs a Laboratoria
// error: TypeError: LAB.despedida is not a function
// Con error o sin error siempre me imprimo!!!

Object.prototype.despedida = function() { return 'Hasta pronto!!!' }

console.log(LAB.despedida());
// Hasta pronto!!!

console.log('despedida' in LAB);
// true

console.log(LAB.hasOwnProperty('despedida'));
// false

delete LAB.saludo
// true

// copiar un Objeto
const newLAB = Object.assign({}, LAB);
```

## Destructuración de Arrays y Objetos

```js
const numbers = ["1", "2", "3"];

const [uno, dos, tres] = numbers;
cl(uno, dos, tres);
// 1 2 3

let one, two, three;
[one, two, three] = ['uno', 'dos', 'tres'];
// ["uno", "dos", "tres"]

const f = () => ['one', 'two', 'three'];
let [uno, dos, tres] = f();
cl(uno, dos, tres);
// one two three

const cl = console.log;

let animal = {
    specie: 'dog',
    sound: 'woof'
};

let { specie, sound } = animal;
cl(`The ${specie} says ${sound}!!!`);

// f1
function makeSound(options) {
  cl(`the ${options.specie} says ${options.sound}!!!`);
};

makeSound({
  specie: 'dog',
  sound: 'woof'
});
// the dog says woof!!!

// f2
function makeSound(options) {
  cl(`the ${options.specie} says ${options.sound}!!!`);
};

makeSound({
  sound: 'woof'
});
// the undefined says woof!!!

// f3
function makeSound(options) {
  options.specie = options.specie || 'dog';
  cl(`the ${options.specie} says ${options.sound}!!!`);
};

makeSound({
  sound: 'woof'
});
// the dog says woof!!!

// f4
function makeSound(options) {
  let specie = options.specie || 'dog';
  let sound = options.sound;
  cl(`the ${specie} says ${sound}!!!`);
};

makeSound({
  sound: 'woof'
});
// the dog says woof!!!

// f5
function makeSound(options) {
  let { specie, sound } = options;
  specie = specie || 'dog';
  cl(`the ${specie} says ${sound}!!!`);
};

makeSound({
  sound: 'woof'
});

// f6
function makeSound({ specie = 'dog', sound }) {
  cl(`the ${specie} says ${sound}!!!`);
};

makeSound({
  sound: 'woof'
});
// the dog says woof!!!
```

## Objetos precompilados

`Number`, `Math`, `Date`, `String`, `Array`, `Boolean`, `Function`, `RegExp`, `Object`, `etc...`
