---
kun: 3
sarlovha: Bizning birinchi komponentlarimiz
---

Birinchi kuni tanishtirgan "Hello world" dasturini qayta ko'rib chiqamiz:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Hello world</title>
  <!-- Script tags including React -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/react/15.3.1/react.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/react/15.3.1/react-dom.min.js"></script>
  <script src="https://npmcdn.com/babel-core@5.8.38/browser.min.js"></script>
</head>
<body>
  <div id="app"></div>
  <script type="text/babel">
    var app = <h1>Hello world</h1>
    var mountComponent = document.querySelector('#app');
    ReactDOM.render(app, mountComponent);
  </script>
</body>
</html>
```

<div id="demo1"></div>

### React kutubxonasini yuklash

Biz React manbasini **(source)** sahifamizning `<head>` elementi ichiga `<script>` tegi sifatida qo'shdik. Biz`<script>` tegi orqali har xil kutubxonalar yuklashdan oldin React kutubxonalarini e'lon qilamiz, aks holda `React` va `ReactDOM` o'zgaruvchilari **(variables)** ularni ishlatishimiz uchun o'z vaqtida aniqlanmaydi.

Shuningdek,`<head>` ichida `babel-core` kutubxonasini o'z ichiga olgan `script` yorlig'i mavjud. Ammo `babel-core` nima?

### Babel

Kecha biz ES5 va ES6 haqida gaplashdik. ES6-ni qo'llab-quvvatlash hali ham aniq emas ekanligini eslatib o'tdik. ES6-dan foydalanish uchun ES6 JavaScript-ni ES5 JavaScript-ga ko'chirib **(transpile)** qo'ysak yaxshi bo'ladi.

**Babel** - ES6-ni ES5-ga ko'chirish uchun kutubxona.

`body` ichida bizda `script` tegi mavjud. `script` ichida biz birinchi React dasturimizni aniqlaymiz. Shuni esda tutingki, `script` yorlig'ida `text/babel` turi **(type)** mavjud:

```html
<script type="text/babel">
```

Bu Bebel ga ushbu `script` tanasi ichidagi JavaScript-ni bajarilishini xohlashimizni bildiradi. Biz o'zimizning React dasturimizni ES6 JavaScript-dan foydalangan holda yozishimiz mumkin va Babel uning bajarilishini faqat ES5-ni qo'llab-quvvatlaydigan brauzerlarda boshqarishi mumkin.

### React app

Babel `script` tanasi ichida biz birinchi React dasturini aniqladik. Bizning dasturimiz bitta elementdan iborat `<h1>Hello world</h1>`. `ReactDOM.render()` ni chaqirishimiz **(call)** aslida bizning kichik React dasturimizni sahifaga joylashtiradi, `ReactDOM.render()` ni chaqirmasak, DOM-da hech narsa ko'rsatilmaydi. `ReactDOM.render()` ning birinchi argumenti _what_, ikkinchisi _where_:

```
ReactDOM.render(<what>, <where>)
```

Biz React dasturini yozdik. Bizning "ilova"(app) - bu `h1` yorlig'ini ifodalovchi React elementidir. Ammo bu unchalik qiziq emas. Boy veb-ilovalar foydalanuvchi ma'lumotlarini qabul qiladi, foydalanuvchining o'zaro ta'siriga qarab shaklini o'zgartiradi va veb-serverlar bilan aloqa o'rnata oladi. Keling, ushbu kuch haqida birinchi React komponentini yaratish orqali tanishaylik.

## Komponentlar va boshqalar

Ushbu ketma-ketlikning boshida biz barcha React dasturlarining markazida _componentlar_ borligini aytib o'tgan edik. React komponentlarini tushunishning eng yaxshi usuli ularni yozishdir. React komponentlarini ES6 sinflari **(class)** sifatida yozamiz.

Keling, biz `App` deb nomlanadigan komponentni ko'rib chiqamiz. Boshqa barcha React komponentlari singari, ushbu ES6 klassi ham React paketidan `React.Component` sinfini uzatadi:

```javascript
class App extends React.Component {
  render() {
    return <h1>Hello from our app</h1>
  }
}
```

> Barcha React komponentlari kamida `render ()` funktsiyasini talab qiladi. Ushbu `render ()` funktsiyasi brauzerning DOM elementiga virtual DOM vakolatini qaytarishi kutilmoqda.

> React komponentasini yozishning bir necha yo'li mavjud. Ushbu ketma-ketlik davomida biz ularni yozishning bir necha usullarini ko'rib chiqamiz. Biz foydalanadigan eng keng tarqalgan shakl - bu yuqorida ishlatilgan ES6 class shakli.
>
> `App` komponentasini yozishning yana bir usuli - bu `React.createClass()` funktsiyasidan foydalanish.
>
> ```javascript
> var App = React.createClass({
>   render: function() {
>     return <h1>Hello from our app</h1>
>   }
> });
> ```
>

Bizning `index.html` da JavaScript kodini oldingi `App` komponentasi bilan almashtiramiz.

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Hello world</title>
  <!-- Script tags including React -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/react/15.3.1/react.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/react/15.3.1/react-dom.min.js"></script>
  <script src="https://npmcdn.com/babel-core@5.8.38/browser.min.js"></script>
</head>
<body>
  <div id="app"></div>
  <script type="text/babel">
//     var app = <h1>Hello world</h1>
//     var mountComponent = document.querySelector('#app');
//     ReactDOM.render(app, mountComponent);
    class App extends React.Component {
      render() {
        return <h1>Hello from our app</h1>
      }
    }
  </script>
</body>
</html>
```
Biroq, ekranda hech narsa ko'rinmaydi. Nimaga esingizdami?

React-ga biz ekranda biror narsa ko'rsatishni yoki _where_-da ko'rsatishni xohlayotganimizni aytmadik. React-ga kerakli narsani va qaerda bo'lishini ko'rsatish uchun yana `ReactDOM.render()` funktsiyasidan foydalanishimiz kerak.

`ReactDOM.render ()` funktsiyasini qo'shish bizning ilovamizni **(application)** ekranga chiqaradi:

```javascript
var mount = document.querySelector('#app');
ReactDOM.render(<App />, mount);
```
<div id="demo2"></div>

E'tibor bering, biz `App` klassidan foydalangan holda React dasturini ichki DOM komponent turi kabi (`<h1 />` va `<div />` teglari kabi) ko'rsatishimiz mumkin. Bu erda biz uni burchakli qavsli element kabi ishlatmoqdamiz: `<App />`.

Bizning React komponentlarimiz xuddi bizning sahifamizdagi boshqa elementlar singari ishlaydi degan fikr bizga xuddi **mahalliy brauzer daraxtini yaratganday komponentlar daraxtini yaratishga** imkon beradi.

Hozir biz React komponentini taqdim qilayotgan bo'lsak ham, bizning dasturimiz hali ham boylik yoki interaktivlikka ega emas. Yaqinda biz React komponentlarini qanday qilib ma'lumotlarga asoslangan **(data-driven)** va dinamik qilishni ko'rib chiqamiz. Avvalo, ushbu ketma-ketlikning navbatdagi qismida biz qanday qilib komponentlarni qatlamlashimiz mumkinligini o'rganamiz. Ichki komponentlar **( Nested components)** boy React veb-dasturining asosi hisoblanadi.