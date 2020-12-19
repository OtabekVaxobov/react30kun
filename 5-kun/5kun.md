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

## props bilan tanishtirish

Reakt bizga ma'lumotni HTML bilan bir xil sintaksisdagi tarkibiy qismga atributlardan yoki _properties_ dan foydalanib yuborish imkonini beradi. Bu `src` atributini image(rasm) yorlig'iga o'tkazishga o'xshaydi. Biz `<img />` yorlig'ining xususiyati haqida `img` deb nomlangan komponentni o'rnatgan `prop` sifatida o'ylashimiz mumkin.

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
