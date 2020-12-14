---
kun: 1
sarlovha: React bu nima?
---
Keyingi 30 kun ichida siz [React] (https://facebook.github.io/react/)
veb-freymvorkining turli qismlari va uning ekotizimi bilan tanishgan bo'lasiz.
Bizning 30 kunlik sarguzashtimizning har kuni oldingi kun materiallariga asoslanadi,
shuning uchun ketma-ketlikning oxiriga kelib siz nafaqat ramka doirida ishlash shartlari,
tushunchalari va asoslarini bilib olasiz, balki o'zingizning veb-dasturingizda React-dan foydalanishingiz mumkin. 
Qani boshladik. Biz [eng boshlang`ich](https://www.youtube.com/watch?v=1RW3nDRmu6k)dan boshlaymiz,
chunki boshlang`ichlar uchun juda yaxshi video.

## React bu nima?

[React](https://facebook.github.io/react/) - bu foydalanuvchi interfeyslarini yaratish uchun JavaScript kutubxonasi. Bu veb-ilovalar uchun ko'rish(view) qatlami.

Barcha React dasturlarining markazida **komponentlar (components)** mavjud. Komponent - bu ba'zi bir natijalarni beradigan mustaqil **(self-contained)** modul. Biz tugma **(button)** yoki kirish(input field) maydoni kabi interfeys elementlarini React komponentasi sifatida yozishimiz mumkin. Komponentlar kompozitsiondir **(composable)**. Komponent o'z tarkibiga bir yoki bir nechta boshqa komponentlarni kiritishi mumkin.

Keng ma'noda, React dasturlarini yozish uchun biz turli xil interfeys elementlariga mos keladigan React komponentlarini yozamiz. Keyinchalik biz ushbu tarkibiy qismlarni dasturimiz tuzilishini belgilaydigan yuqori darajadagi **(higher-level)** tarkibiy qismlar ichida tashkil qilamiz.

Masalan, shaklni oling. Shakl ko'plab interfeys elementlaridan iborat bo'lishi mumkin, masalan kirish maydonlari **(input fields)**, yorliqlar **(labels)** yoki tugmalar **(buttons)**. Shakl ichidagi har bir element React komponentasi sifatida yozilishi mumkin. Keyinchalik biz yuqori darajadagi komponentni, ya'ni shakl komponentasini yozamiz. Forma komponentasi shaklning tuzilishini aniqlaydi va uning ichiga ushbu interfeys elementlarining har birini kiritadi.

Muhimi, React dasturidagi har bir komponent ma'lumotlar boshqaruvining qat'iy **(strict)** tamoyillariga amal qiladi **(strict data management principles)**. Murakkab, interfaol foydalanuvchi interfeyslari ko'pincha murakkab ma'lumotlar va dastur holatini **(state)** o'z ichiga oladi. React-ning sirt maydoni cheklangan va bizning dasturimiz muayyan sharoitlarda qanday ko'rinishini oldindan bilishimiz uchun vositalarni berishga qaratilgan. Keyinchalik ushbu printsiplarni o'rganamiz.

## Yaxshi, biz uni qanday ishlatamiz?

Reakt - bu JavaScript freymvorki. Freymvorkdan foydalanish JavaScript-faylni HTML-ga qo'shish va dasturimizning JavaScript-dagi `React` eksportidan foydalanish kabi oddiy.

Masalan, React veb-saytining _Hello world_ misoli oddiy bo'lishi mumkin:

```html
<html>
<head>
  <meta charset="utf-8">
  <title>Hello world</title>
  <!-- Reaktni o'z ichiga olgan skript teglari -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/react/15.3.1/react.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/react/15.3.1/react-dom.min.js"></script>
  <script src="https://npmcdn.com/babel-core@5.8.38/browser.min.js"></script>
</head>
<body>
  <div id="app"></div>
  <script type="text/babel">
    ReactDOM.render(
      <h1>Hello world</h1>,
      document.querySelector('#app')
    );
  </script>
</body>
</html>
```

<div id="demo1"></div>

Biroz qo'rqinchli ko'rinishi mumkin bo'lsa-da, JavaScript kodi _Hello world_ sahifasiga dinamik ravishda qo'shadigan bitta satr. Shuni yodda tutingki, biz hamma narsani ishlashi uchun faqat bir nechta JavaScript-fayllarni kiritishimiz kerak edi.

## Bu qanday ishlaydi?

Ko'pgina avvalgilaridan farqli o'laroq, React to'g'ridan-to'g'ri brauzerning Document Object Model (DOM) da emas, balki **virtual DOM** da ishlaydi. Ya'ni, bizning ma'lumotlarimizdagi o'zgarishlardan so'ng (bu juda sekin bo'lishi mumkin) brauzerda `document` bilan ishlashdan ko'ra, u o'zining virtual DOM-dagi o'zgarishlarni hal qiladi. Virtual DOM yangilanganidan so'ng, React haqiqiy DOMga qanday o'zgartirish kiritilishini aniq belgilaydi.

[React Virtual DOM](https://facebook.github.io/react/docs/dom-differences.html) to'liq xotirada mavjud va veb-brauzerning DOM-ning vakili. Shu sababli, biz React komponentasini yozganimizda, biz to'g'ridan-to'g'ri DOMga yozmaymiz, lekin biz React DOMga aylanadigan virtual komponentni yozamiz.