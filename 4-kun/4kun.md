---
kun: 4
sarlovha: Bizning birinchi komponentlarimiz
---

_React 30 kunda_ ning oldingi qismida biz birinchi React komponentini yaratishni boshladik. Ushbu bo'limda biz o'z ishimizni `App` komponentasi bilan davom ettiramiz va yanada murakkab interfeysni yaratishni boshlaymiz.

Biz ko'rishimiz mumkin bo'lgan umumiy veb-element - bu foydalanuvchi xronologiyasi. Masalan, bizda Facebook va Twitter kabi dasturlar kabi voqealar tarixini ko'rsatadigan dastur bo'lishi mumkin.

Ushbu interfeysni bitta komponentda qurishimiz mumkin. Biroq, bitta dasturda butun dasturni yaratish ajoyib g'oya emas, chunki u ulkan, murakkab va testlardan o'tishi qiyin.

```javascript

//Kod faqat misol uchun, yozish shart emas
// code/timeline1.jsx
// .jsx faylni odiygina brauzer bilan ochib bo'lmaydi
// node.js va npm server kerak bo`ladi
class Panel extends React.Component {
  render() {
    return (
      <div className="notificationsFrame">
        <div className="panel">
          <div className="header">
            
            <div className="menuIcon">
              <div className="dashTop"></div>
              <div className="dashBottom"></div>
              <div className="circle"></div>
            </div>

            <span className="title">Timeline</span>

            <input
              type="text"
              className="searchInput"
              placeholder="Search ..." />

            <div className="fa fa-search searchIcon"></div>
          </div>
          <div className="content">
            <div className="line"></div>
            <div className="item">

              <div className="avatar">
                <img src="http://www.croop.cl/UI/twitter/images/doug.jpg" />
                Doug
              </div>

              <span className="time">
                An hour ago
              </span>
              <p>Ate lunch</p>
            </div>

            <div className="item">
              <div className="avatar">
                <img src="http://www.croop.cl/UI/twitter/images/doug.jpg" />
              </div>

              <span className="time">10 am</span>
              <p>Read Day two article</p>
            </div>

            <div className="item">
              <div className="avatar">
                <img src="http://www.croop.cl/UI/twitter/images/doug.jpg" />
              </div>

              <span className="time">10 am</span>
              <p>Lorem Ipsum is simply dummy text of the printing and typesetting industry.</p>
            </div>

            <div className="item">
              <div className="avatar">
                <img src="http://www.croop.cl/UI/twitter/images/doug.jpg" />
              </div>

              <span className="time">2:21 pm</span>
              <p>Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.</p>
            </div>

          </div>
        </div>
      </div>
    )
  }
}
```
<div class="demo" id="demo1"></div>

## Bo'laklarga bo'lish

Buni bitta komponentda joylashimizdan ko'ra, uni bir nechta komponentlarga bo'lamiz.

Ushbu komponentni ko'rib chiqsak, kattaroq tarkibiy qism uchun ikkita alohida qism mavjud ekanligi ko'ramiz(1-rasm):

1. Sarlavha satri(title bar)
2. Asosiy qism(content)

Biz tarkibiy qismlarning mazmunini alohida ajraladigan qismlarga bo'lishimiz mumkin. Tarkib qismida 3 xil _item_ komponent mavjud(2-rasm).

> Agar biz bir qadam oldinga borishni xohlasak, hatto sarlavha satrini 3 qismga, _menu_ tugmasi, _title_ va _search_ belgisiga ajratishimiz mumkin. Agar kerak bo'lsa, biz ularning har biriga yanada ko'proq sho'ng'iy olamiz.

## Konteyner komponenti

Xabarnomalar dasturini **(notifications app)** yaratish uchun avval butun dasturni saqlash uchun konteyner qurishdan boshlaymiz. Bizning konteynerimiz shunchaki boshqa ikkita komponent uchun "o'ralgan" bo'ladi.

Ushbu komponentlarning hech biri maxsus funktsiyonallarni talab qilmaydi (hali), shuning uchun ular bizning `HelloWorld` komponentimizga o'xshaydi, chunki u faqat bitta renderlash funktsiyasiga ega komponent hisoblanadi.

Biz shunga o'xshash ko'rinishi mumkin bo'lgan `App` deb nomlanadigan _wrapper_ komponentini yarataylik:
```javascript
//code/container.jsx
class App extends React.Component {
  render() {
    return (
      <div className="notificationsFrame">
        <div className="panel">
          {/* content goes here */}
        </div>
      </div>
    )
  }
}
```
> E'tibor bering, biz `class` ning HTML versiyasi o'rniga React-da `className` deb nomlangan atributdan foydalanmoqdamiz. Shuni yodda tutingki, biz DOMga to'g'ridan-to'g'ri yozmayapmiz va shuning uchun HTML emas, balki JSX (bu faqat JavaScript).
>
> `ClassName` dan foydalanishimizning sababi shundaki, `class` JavaScript-da zaxiralangan so'zdir.

## Farzand komponentalar(Child components)

Agar komponent boshqa komponent ichiga joylashtirilsa, u _child_ komponentasi deb nomlanadi. Komponentda bir nechta farzand komponentlari bo'lishi mumkin. Farzand komponentini ishlatadigan komponent keyinchalik _parent_ komponentasi deb nomlanadi.

Belgilangan komponent bilan biz `title` va `content`tarkibiy qismlarini manbani asl dizaynimizdan olish va har bir komponentga manba faylini joylashtirish orqali yaratishimiz mumkin.

Masalan, sarlavha(header) komponentasi quyidagicha ko'rinadi, konteyner elementi bilan `<div className ="header"> `, menyu belgisi, sarlavha va qidiruv satri:

```javascript
//code/header.jsx
class Header extends React.Component {
  render() {
    return (
      <div className="header">
        <div className="fa fa-more"></div>

        <span className="title">Timeline</span>

        <input
          type="text"
          className="searchInput"
          placeholder="Search ..." />

        <div className="fa fa-search searchIcon"></div>
      </div>
    )
  }
}
```
<div class="demo" id="headerDemo"></div>

Va nihoyat, biz `Content` komponentini vaqt jadvallari bilan yozishimiz mumkin. Har bir vaqt jadvalining elementi bitta komponentga o'ralgan, u bilan bog'langan avatar, vaqt tamg'asi(timestamp) va ba'zi matnlar mavjud.

```javascript
//code/contaent1.jsx
class Content extends React.Component {
  render() {
    return (
      <div className="content">
        <div className="line"></div>

      {/* Timeline item */}
        <div className="item">
          <div className="avatar">
            <img src="http://www.croop.cl/UI/twitter/images/doug.jpg" />
            Doug
          </div>

          <span className="time">
            An hour ago
          </span>
          <p>Ate lunch</p>
          <div className="commentCount">
            2
          </div>
        </div>

        {/* ... */}

      </div>
    )
  }
}
```
> React komponentiga komentariya(sharh) yozish uchun biz uni qavsga JavaScript-dagi ko'p satrli komentariya sifatida joylashtirishimiz kerak.

## Barchasini birlashtiramiz

Endi bizda ikkita _children_ komponentlari mavjud bo'lib, biz `Header` va `Content` qismlarini `App` komponentasining _children_ bo'lishini o'rnatishimiz mumkin. Keyin bizning `App` komponentimiz ushbu komponentlardan _go'yo ular brauzerga o'rnatilgan HTML elementlari_ sifatida ishlatishi mumkin. Sarlavha va tarkibga ega bo'lgan yangi `App` komponentimiz quyidagicha:

```javascript
//code/container2.jsx
class App extends React.Component {
  render() {
    return (
      <div className="notificationsFrame">
        <div className="panel">
          <Header />
          <Content />
        </div>
      </div>
    )
  }
}
```
<div class="demo" id="demo2"></div>

Ushbu bilim bilan endi biz bir nechta tarkibiy qismlarni yozish qobiliyatiga egamiz va biz yanada murakkab dasturlarni yaratishni boshlashimiz mumkin.

Shu bilan birga, ushbu dasturda foydalanuvchilarning o'zaro aloqasi yoki maxsus ma'lumotlari yo'qligini sezish mumkin. Darhaqiqat, hozirda bizning React dasturimiz oddiy, lekin oddiy HTML-ga qaraganda oson emas.

Keyingi bo'limda biz qanday qilib o'zimizning komponentimizni yanada dinamik qilishini va react yordamida _data-driven_ yo'llarini ko'rib chiqamiz.