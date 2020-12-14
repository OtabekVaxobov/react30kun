---
kun: 2
sarlovha: JSX nima?
---

Avvalgi maqolamizda [React](https://facebook.github.io/react/) nima ekanligini ko'rib chiqdik va uning qanday ishlashini yuqori darajada **(high-level)** muhokama qildik. Ushbu maqolada biz React ekotizimining bir qismini ko'rib chiqamiz: ES6 va JSX.

## JSX/ES5/ES6 WTF??!

Internetda React materialini qidiradigan har qanday jiddiy qidiruvda, shubhasiz siz allaqachon `JSX`, `ES5` va `ES6` atamalarini ishlatgansiz. Ushbu shaffof bo'lmagan qisqartmalar tezda chalkashib ketishi mumkin.

ES5 (`ES` ECMAScript degan ma'noni anglatadi) asosan `oddiy JavaScript` dir. Javascript, ES5-ning 5-yangilanishi 2009 yilda nihoyasiga yetdi. Bir necha yildan beri barcha yirik brauzerlar tomonidan qo'llab-quvvatlanib kelinmoqda. Shuning uchun, agar siz yaqin o'tmishda biron bir JavaScript-ni yozgan bo'lsangiz yoki ko'rgan bo'lsangiz, ehtimol ES5 bo'lishi mumkin.

ES6 - bu JavaScript-ning yangi versiyasi bo'lib, u juda yaxshi sintaktik va funktsional qo'shimchalar qo'shadi. 2015 yilda yakunlandi. ES6 barcha asosiy brauzerlar tomonidan [deyarli to'liq qo'llab-quvvatlanadi](http://kangax.github.io/compat-table/es6/). Ammo veb-brauzerlarning eski versiyalari bekor qilinmaguncha biroz vaqt ketadi. Masalan, Internet Explorer 11 ES6-ni qo'llab-quvvatlamaydi, ammo brauzer bozorining taxminan 12% ulushiga ega.

Bugungi kunda ES6-ning afzalliklaridan foydalanish uchun biz uni iloji boricha ko'proq brauzerlarda ishlashi uchun bir nechta narsani qilishimiz kerak:

1. Ko'proq brauzerlar bizning JavaScript-ni tushunishlari uchun biz kodimizni _transpile_ qilishimiz kerak. Bu ES6 JavaScript-ni ES5 JavaScript-ga o'zgartirishni anglatadi.
2. Biz brauzerda bo'lishi mumkin yoki bo'lmasligi mumkin bo'lgan ES6 ga qo'shimcha funktsiyalarni ta'minlaydigan _shim_ yoki _polyfill_ ni kiritishimiz kerak.

Buni qanday amalga oshirganimizni biroz keyinroq ko'ramiz.

> Ushbu ketma-ketlikda yozadigan kodlarning aksariyati ES5-ga osonlikcha tarjima qilinadi. Biz ES6-dan foydalanadigan holatlarda dastlab ushbu funktsiyani kiritamiz, so'ngra u orqali o'tamiz.

Ko'rib turganimizdek, bizning barcha React komponentlarimiz `render` funktsiyasiga ega, bu bizning React komponentamizning HTML chiqishi **(output)** qanday bo'lishini belgilaydi. **JavaScript eXtension**, yoki kengroq **JSX** - bu React kengaytmasi bo'lib, bizga HTMLga o'xshaydigan JavaScript yozish imkonini beradi.

> Avvalgi paradigmalarda JavaScript-ni va formatlashni bir joyga qo'shish yomon odat sifatida ko'rilgan bo'lsa-da, ko'rinishni funksionallik bilan birlashtirish to'g'ridan-to'g'ri ko'rinish haqida fikr yuritadi.

Buning tushunish uchun bizda `h1` HTML yorlig'i ko'rsatadigan React komponenti borligini tasavvur qiling. JSX ushbu elementni HTML ga o'xshash tarzda e'lon qilishga imkon beradi:

{lang=javascript,crop-query=.Header}
<<[](HelloWorldJSX.js)

<div id="demo1"></div>

`HelloWorld` komponentidagi `render()`funktsiyasi HTML-ni qaytarganga **(return)** o'xshaydi, lekin bu aslida JSX. JSX ish paytida oddiy JavaScript-ga o`giriladi _translated_. Ushbu komponent tarjima qilinganidan so'ng quyidagicha ko'rinadi:

```javascript
class HelloWorld extends React.Component {
  render() {
    return (
      React.createElement(
        'h1',
        {className: 'large'},
        'Hello World'
      )
    );
  }
}
```
JSX HTMLga o'xshash bo'lsa-da, aslida bu `React.createElement()` deklaratsiyasini yozishning oddiy usuli. Komponent ko'rsatilganda u React elementlari daraxtini yoki ushbu komponentning HTML elementlarini **virtual representation** **(virtual vakolatini)** chiqaradi. Keyin React ushbu React elementi asosida haqiqiy DOMga qanday o'zgarishlar kiritilishini aniqlaydi. `HelloWorld` komponentasida, React DOM-ga yozadigan HTML quyidagicha bo'ladi:

```html
<h1 class='large'>Hello World</h1>
```

> React birinchi komponentimizda ishlatilgan `class extends` sintaksisi ES6 sintaksisidir. Bu bizga tanish Ob'ektga yo'naltirilgan(Object-Oriented) uslub yordamida ob'ektlarni yozish imkonini beradi.
> ES5 da `class` sintaksisini quyidagicha tarjima qilish mumkin:
>
> ```javascript
> var HelloWorld = function() {}
> Object.extends(HelloWorld, React.Component)
> HelloWorld.prototype.render = function() {}
> ```

JSX JavaScript-ni bo'lgani uchun biz JavaScript-ga zaxiralangan so'zlardan **(reserved words)** foydalana olmaymiz. Bunga `class` va `for` kabi so'zlar kiradi.

React bizga `className` atributini beradi. Biz uni `HelloWorld` da `h1` yorlig'imizga `large` sinfini **(class)** o'rnatish uchun ishlatamiz. Yana bir nechta atributlar mavjud, masalan, yorliqdagi `for` atributi, chunki React `htmlFor` ga `for` deb tarjima qilinadi, shuningdek, zaxiralangan so'z. Ularni ishlatishni boshlaganimizda, ularni ko'rib chiqamiz.

Agar biz JSX kompilyatoriga ishonish o'rniga sof JavaScript-ni yozmoqchi bo'lsak, shunchaki `React.createElement ()` funktsiyasini yozishimiz va abstraktsiya qatlami haqida qayg'urmasligimiz mumkin. Lekin bizga JSX yoqadi. Ayniqsa, murakkab tarkibiy qismlar bilan ko'proq o'qishi mumkinligi uchun. Quyidagi JSX-ni ko'rib chiqing:

```javascript
<div>
  <img src="profile.jpg" alt="Profile photo" />
  <h1>Welcome back Ari</h1>
</div>
```

Brauzerga etkazilgan JavaScript quyidagicha bo'ladi:

```javascript
React.createElement("div", null, 
  React.createElement("img", {src: "profile.jpg", alt: "Profile photo"}),
  React.createElement("h1", null, "Welcome back Ari")
);
```

Shunga qaramay, siz JSX-ni o'tkazib yuborishingiz va ikkinchisini to'g'ridan-to'g'ri yozishingiz mumkin bo'lsa-da, JSX sintaksisi ichki **(nested)** HTML elementlarini namoyish qilish uchun juda mos keladi.

Endi biz JSXni tushunganimizdan so'ng, biz birinchi React komponentlarini yozishni boshlashimiz mumkin. Ertaga biz birinchi React dasturimizga o'tishda bizga qo'shiling.