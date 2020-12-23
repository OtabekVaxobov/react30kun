---
kun: 5
sarlovha: Ma'lumotlarga asoslangan(Data-Driven)
---

Shu nuqtagach biz birinchi tarkibiy qismlarimizni yozdik va ularni **child/parent** munosabatlarida ko'rib chiqdik. Biroq, biz hali ham React tarkibiy qismlariga hech qanday ma'lumot bog'lamadik. React-da veb-sayt yozish (bizning fikrimizcha) yoqimli tajriba bo'lsa-da, biz biron bir dinamik ma'lumotlarni namoyish qilish uchun React kuchidan foydalanmadik.

## Ma'lumotlarga asoslangan holda olg'a

Eslatib o'tamiz, kecha biz `header`, `activity` qismlarini o'z ichi oluvchi `timeline` komponentasini boshladik.

Biz demoimizni tarkibiy qismlarga ajratdik va statik JSX shablonlari(templates) bilan uchta alohida komponentni yaratdik. Bizning veb-saytimiz ma'lumotlari o'zgarganida har doim tarkibiy qism shablonini yangilashimiz juda qulay emas.

Buning o'rniga, aks ettirish uchun ishlatiladigan komponentlarga ma'lumot beraylik. `<Header />` komponentidan boshlaymiz. Hozirda `<Header />`  komponentasi elementning sarlavhasini faqat `Timeline` sifatida ko'rsatadi. Bu juda yaxshi element va uni sahifamizning boshqa qismlarida qayta ishlatsak yaxshi bo'lar edi, ammo `Timeline` sarlavhasi har foydalanish uchun mantiqiy emas.

Reaktga aytaylik, sarlavhani boshqa narsaga o'rnatishni xohlaymiz.

## props bilan tanishamiz

Reakt bizga ma'lumotni HTML bilan bir xil sintaksisdagi tarkibiy qismga atributlardan yoki _properties_ dan foydalanib imkonini beradi. Bu `src` atributini image(rasm) yorlig'iga o'tkazishga o'xshaydi. Biz `<img />` yorlig'ining xususiyati haqida `img` deb nomlangan komponentni o'rnatgan `prop` sifatida o'ylashimiz mumkin.

Ushbu xususiyatlarga komponent ichida `this.props` sifatida kirishimiz mumkin. Keling, `props` ni amalda ko'rib chiqamiz.

Eslatib o'tamiz, biz `<Header />` komponentini quyidagicha yozgan edik:

```javascript
class Header extends React.Component {
  render() {
    return (
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
    )
  }
}
```
`<Header />` komponentidan foydalanganda, uni `<App />` komponentamizga quyidagicha joylashtirdik:

```javascript
<Header />
```
Biz `title` ni `<Header />` ga atribut sifatida **parametr(sifat)** yani props qilib o'tishimiz mumkin, masalan:

```javascript
<Header title="Timeline" />
```
Komponentimiz ichida yani `Header` ichidagi `title` ga `this.props` xususiyatini berishimiz mumkin. Shablonda sarlavhani statik ravishda `Timeline` deb belgilash o'rniga, uni o'zgartiriladigan xususiyat(property) bilan almashtirishimiz mumkin.

```javascript
class Header extends React.Component {
  render() {
    return (
      <div className="header">
        <div className="menuIcon">
          <div className="dashTop"></div>
          <div className="dashBottom"></div>
          <div className="circle"></div>
        </div>

        <span className="title">
          {this.props.title}
        </span>

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
> Shuningdek, biz so'nggi `<Header />` kodimiz ko'rinishiga yaqinlashish uchun kodni biroz yangiladik, jumladan `searchIcon` va `menuIcon` stilini yaratish uchun bir nechta elementlarni qo'shdik.

Endi bizning `<Header />` komponentasi biz komponentni chaqirganimizda biz kiritgan satrni `title` sifatida aks ettiradi. Masalan, `<Header />` tarkibiy qismiga to'rt marta chaqirish shunday ko'rinishda:

```javascript
<Header title="Timeline" />
<Header title="Profile" />
<Header title="Settings" />
<Header title="Chat" />
```
Biz `componet` ga oddiy satr(string) dan tashqari ko'p narsalar ishlatishimiz mumkin. Biz raqamlar, satrlar, barcha turdagi ob'ektlar va hatto funktsiyalarni `title` o'rniga ishlatishimiz mumkin! Ushbu turli xil xususiyatlarni qanday ishlatish kerakligi haqida ko'proq gaplashamiz, keyinroq api komponentini yaratishimiz mumkin.

Tarkibni va sanani statik ravishda belgilash o'rniga `Content` komponentini olamiz va vaqt jadvalini tarkibini matn o'rniga ma'lumotlar o'zgaruvchisi bilan o'rnatamiz. Xuddi HTML komponentlari bilan ishlashimiz singari, biz ham bir nechta `props` komponentaga o'tkaza olamiz.

Eslatib o'tamiz, kecha biz `Content` konteynerimizni quyidagicha aniqladik:

```javascript
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
Keling `title` bilan qilganimiz kabi, `Content` tarkibiy qismimiz uchun `props` nima kerakligini ko'rib chiqaylik:

* Foydalanuvchining avatar tasviri
* Faoliyat vaqti
* Faoliyat elementining matni
* Izohlar soni

Aytaylik, bizda faoliyat elementini ifodalovchi JavaScript ob'ekti mavjud. Bizda qatorlar (matn) va sana ob'ekti kabi bir nechta maydonlar bo'ladi. Bizda `user` va `comments` kabi ba'zi bir ichki ob'ektlar bo'lishi mumkin. Masalan:

```javascript
{
  timestamp: new Date().getTime(),
  text: "Ate lunch",
  user: {
    id: 1,
    name: 'Nate',
    avatar: "http://www.croop.cl/UI/twitter/images/doug.jpg"
  },
  comments: [
    { from: 'Ari', text: 'Me too!' }
  ]
}
```
Xuddi biz `<Header />` komponentasida `title`ning matnini ishlatganimiz kabi, endi ushbu faoliyat ob'ektini olib, uni to'g'ridan-to'g'ri `Content` komponentasiga o'tkazamiz. Keling, ushbu faoliyat tafsilotlarini shablon ichida ko'rsatish uchun tarkibiy qismimizni o'zgartiraylik.

Shablonga dinamik o'zgaruvchining(variable) qiymatini o'tkazish uchun biz uni shablonimizda ko'rsatish uchun shablon sintaksisidan foydalanishimiz kerak. Masalan:

```javascript
class Content extends React.Component {
  render() {
    const {activity} = this.props; // ES6 destruktizatsiyasi

    return (
      <div className="content">
        <div className="line"></div>

        {/* Timeline item */}
        <div className="item">
          <div className="avatar">
            <img
              alt={activity.text}
              src={activity.user.avatar} />
            {activity.user.name}
          </div>

          <span className="time">
            {activity.timestamp}
          </span>
          <p>{activity.text}</p>
          <div className="commentCount">
            {activity.comments.length}
          </div>
        </div>
      </div>
    )
  }
}
```

> class imizda ozgina ES6 dan foydalanib, _destructuring_ deb nomlangan `render ()` funktsiyasining birinchi qatorida foydalandik. Quyidagi ikkita satr funktsional jihatdan tengdir:
>
> ```javascript
> // ikkala kod bir xildir:
> const activity = this.props.activity;
> const {activity} = this.props;
> ```
> Tahrirlash(Destructuring) bizni yozishda tejashga imkon beradi va o'zgaruvchilarni qisqa va ixcham tarzda belgilaydi.

Keyinchalik, ushbu yangi tarkibni qattiq kod(hard-code) o'rniga tayanch sifatida ob'ektga yuborish orqali ishlatishimiz mumkin. Masalan:

```javascript
<Content activity={moment1} />
```

Ajoyib, endi biz ob'ektni boshqaradigan(driven) faoliyat elementiga egamiz. Ammo, siz buni bir necha bor turli xil sharhlar bilan amalga oshirishimiz kerakligini sezgan bo'lishingiz mumkin. Buning o'rniga biz bir qator ob'ektlarni tarkibiy qismga o'tkaza olamiz.