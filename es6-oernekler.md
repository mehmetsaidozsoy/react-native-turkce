# ES6 ve ES7 Örnekler

## Block Scoped Declaration

```javascript
const a = 1
let b = 'foo'

// Not allowed!
// a = 2

// Ok!
b = 'bar'

if (true) {
  const a = 3
}
```

**const** ve **let** ifadelerine bakalım. Normal JavaScript'te bu ifadeler yerine değişkenleri tanımlamak için **var** kullanılır. Aralarındaki temel fark **const** ve **let** ifadeleri yalnızca bulundukları blok için geçerlidir.

**const** bildiğimiz "CONSTANT" kelimesinin kısaltması, sabit yani tanımlandığı blokta kendisine yalnızca bir kere atama yapılabilir

**let** ifadesi değişkenler için uygundur. Yukarıdaki örnekte üst blokta tanımlanmış `const "a"`ifadesine bir kere atama yapılmış daha sonra başka bir değişiklik yapılınca buna izin verilmemiş. ama farklı bir blokta tekrar atama yapılabilmiştir.

## Arrow Function \( =&gt; \)

Arrow \(=&gt;\) ya da fat arrow function \(==&gt;\) denilen bu fonksiyon başta kafa karıştırıcı olabilir. Normal bir fonksiyondan temel anlamda bir kaç tane farkı vardır.

Birincisi; ES5 ile yazılmış bir JavaScript kodunda, bir fonksiyonu bind etmek için kullandığımız, `this` kodu eğer biz arrow function kullanıyorsak gerekli değildir. Çünkü arrow function için fonksiyonun kendi bloğu ya da dış blok aynı kapsamdadır.Bir örnekle bakalım;

```javascript
//ES5:
 function merhaba(){
    this.msj = 'Merhaba';
    this.selamver = function(adi){
       return this.msj + adi
    }.bind(this)
 }

 //ES6:
 function merhaba(){
    this.msj = 'Merhaba';
    this.selamver = (adi) =>{
       return this.msj + adi
    }
 }
```

ES5 ile yazılan örnekte `selamver` fonksiyonu kendi üst bloğundaki `msj` 'a ulaşmak için `bind` edilmesi gerekirken; ES6 ile yazılan halinde, arrow function kullanılmış ve `bind` edilmesine gerek kalmadan `msj` değişkenine ulaşılmıştır

İkincisi; Eğer fonksiyonunuz bir parametre alıyorsa, süslü parantez `{}` ve `return` kullanmanıza gerek yok. Kullanırsanız da bir şey değişmez. Örneğin;

```javascript
var half = function(x){
  return x/2
}

var halfES6 = (x)=>{
  return x/2
}

var halfES6_2 = ( x => x/2 )


half(6);     //3
halfES6(8);  //4
halfES6_2(10); //5
```

\[\[[http://jsbin.com/docuhuy/2/embed?live\]\(http://jsbin.com/docuhuy/2/embed?live"&gt;JS\]\(http://jsbin.com/docuhuy/2/embed?live\]%28http://jsbin.com/docuhuy/2/embed?live"&gt;JS\)\](http://jsbin.com/docuhuy/2/embed?live]%28http://jsbin.com/docuhuy/2/embed?live">JS]%28http://jsbin.com/docuhuy/2/embed?live]%28http://jsbin.com/docuhuy/2/embed?live">JS%29\)\)

## Modüller

```javascript
//Modülleri import etme işlemi

//ES5;
var ReactNative = require('react-native');

//ES6;
import ReactNative from 'react-native'
```

```javascript
//Modülleri export etme işlemi

//ES5;
module.exports=(App)

//ES6;
export default App;
export {View, Text, Image } ;
```

## Default Parametre

```javascript
const printAnimal = (animal = 'cat') => {
  console.log(animal)
}
printAnimal() // cat
printAnimal('dog') // dog
```

## Class

ES5 ' de, `class` yaratmak için sadece fonksiyon kullanabiliriz ve`MyFunction.prototype` ile method atıyabiliriz. ES6, `class` için bize daha kolay bir sentaks veriyor.

ES6 bize javascript ile nesneye yönelik programlama imkânı veriyor. `inheritance` yapmak, `static` ve `instance` fonksiyonlar oluşturmak mümkün. Bide bir tane özel bir fonksiyonumuz var; `constructor` . `constructor`, bir class yaratıldığında otomatik olarak çağrılır. Ayrıca `static` kodu ile de static class fonksiyonlar tanımlayabiliriz. inheritance için de kullandığımız keyword, `extends`

```javascript
class Animal {
  constructor(name) {
    this.name = name
  }

  static beProud() {
    console.log('I AM AN ANIMAL')
  }

  printName() {
    console.log(this.name)
  }
}

const animal = new Animal('Cat')
animal.printName() // Cat
Animal.beProud() // I AM AN ANIMAL
```

```javascript
class Cat extends Animal {
      printName() {
        super.printName()
        console.log(`My name is ${this.name}`)  //ES6'nın güzelliklerinden concat işlemine dikkat ediniz `${}`
      }
    }
```

## Array Spread

```javascript
const arabalar = ['mercedes','fiat','bmw']
const yeniArabalar = [...arabalar]  //arabalar dizisinin elemalarıyla, yeni bir dizi oluşturduk
//arabalar = yeniarabalar

const birSuruAraba = [...arabalar, 'kartal','tempra','lada'] //arabalar dizisiyle birlikte, yeni arabalar ekleyip birSuruAraba dizisini oluşturduk

const meyveler = [
   {adi:'muz', renk:'sarı'},
   {adi:'elma', renk:'kırmızı'}, 
]
const yeniMeyveler = [...meyveler]
console.log(yenimeyveler[0].adi) //muz

yeniMeyveler[0].adi = 'ayva'
console.log(yenimeyveler[0].adi) //ayva
```

## Static Variables Class

```javascript
class Cat {
  static legCount = 4
}
console.log(Cat.legCount) // 4
```

## Object Spread

ES6 daki Array Spread gibi, Object Spread `...` objenin elemanlarını dağıtır. ES7 ile gelen bir özelliktir.

{...originalObj} bu bizim ilk objemiz olsun. Biz bunu Object Spread ile kopyasını alıp, istediğimiz bir özelliğini değiştirerek yeni objemizi yaratalım.

```javascript
const cat = {
  name: 'Luna',
  friends: {best: 'Ellie'},
  legs: 4,
}
const strangeCat = {...cat, legs: 6} 
//cat objesinin kopyası şeklinde yeni bir obje yaratacakken, legs özelliğini yeni objemizde değiştirdik
```

## Async ve Await

Asenkron iş planına sahip uygulamamızı hem daha mantıklı hem de daha okunur kılan async , ES7 ile gelmiştir. `await` de onunla beraber kullanılır. async fonksiyonu, asenkron operasyon tamamlanana veya hata alana kadar bir sonraki kod bloğunun çalışmasını engeller.

```javascript
const taskRunner = async () => {
  try {
    const firstValue = await asyncTask1()
    const secondValue = await asyncTask2(firstValue)
  } catch(e) {
    console.error("Bir şeyler ters gitti sanki", e)
  }
}
```

## ES6 Generator

Aşamalı, iterative biçimde ilerlemesi gereken bir fonksiyona ihtiyaç duyuyorsanız ES6 generator ler tam size göre.

```javascript
function* greet(){
   console.log('You called greet');
   yield "hello";
   yield "world";
}

console.log('start')
let greeter =  greet();
let next = greeter.next();
console.log(next)
let done = greeter.next();
console.log(done)

// console' a yazan değerler
/*
"start"
"You called greet"
[object Object] {
  done: false,
  value: "hello"
}
[object Object] {
  done: false,
  value: "world"
}
[object Object] {
  done: true,
  value: undefined
}
*/
```

Tüm generator işlemlerini sırayla yapılmasını istiyorsanız

```javascript
for (let word of greeter){
      console.log(word);
}

// console' a yazılan
"start"
"You called greet"
"hello"
"world"
```

