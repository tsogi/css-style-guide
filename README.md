# ეარბიენბის CSS / Sass სტილისტური სახელმძღვანელო

*ძირითადად გონივრული მიდგომები CSS-სა და Sass-თან დაკავშირებით*

## შინაარსი

1. [ტერმინოლოგია](#terminology)
    - [ინსტრუქციის გამოცხადება](#rule-declaration)
    - [სელექტორები](#selectors)
    - [მახასიათებლები](#properties)
1. [CSS](#css)
    - [გაფორმება](#formatting)
    - [კომენტარები](#comments)
    - [OOCSS და BEM](#oocss-and-bem)
    - [ID Selectors](#id-selectors)
    - [JavaScript hooks](#javascript-hooks)
    - [საზღვრები](#border)
1. [Sass](#sass)
    - [სინტაქსი](#syntax)
    - [თანმიმდევრობა](#ordering-of-property-declarations)
    - [ცვლადები](#variables)
    - [Mixins](#mixins)
    - [Extend directive](#extend-directive)
    - [Nested selectors](#nested-selectors)
1. [თარგმანები](#translation)
1. [ლიცენზია](#license)

## ტერმინოლოგია

### ინსტრუქციის გამოცხადება

ინსტრუქცია არის სელექტორის(ან სელექტორების ჯგუფის) სახელისა და მახახასიათებლების ერთობლიობა რომელსაც აქვს შემდეგი სახე:

```css
.listing {
  font-size: 18px;
  line-height: 1.2;
}
```

### სელექტორები

ინსტრუქციის გამოცხადებისას, "სელექტორები" განსაზღვრავენ თუ DOM-ის რომელ ელემენტებზე გავრცელდება მითითებული მახასიათებლები. სელექტორი შეიძლება განისაზღვროს HTML ელემენტის, ელემენტის კლასის, აიდის ან მისი რომელიმე ატრიბუტის მეშვეობით. ქვემოთ მოყვანილია რამდენიმე მაგალითი:

```css
.my-element-class {
  /* ... */
}

[aria-hidden] {
  /* ... */
}
```

### მახასიათებლები

და ბოლოს, მახასიათებლები ანიჭებენ სელექტორებით არჩეულ ელემენტებს სტილს. თითოეული მახასიათებელი შედგება სახელისა და მნშვნელობისაგან, ნებისმიერი ინსტრუქცია შეიცავს ერთ ან რამდენიმე მახასიათებელს. მაგალითად: 

```css
/* some selector */ {
  background: #f1f1f1;
  color: #333;
}
```

**[⬆ დასაწყისში ასვლა](#table-of-contents)**

## CSS

### გაფორმება

* გამოიყენე მარტივი tab(2 გამოტოვება) სტრიქონის დაწყებისას.
* კლასის სახელის განსაზღვრისას უპირატესობა მიანიჭე ტირეს და არა camelCase-ს.
  - ქვედა ტირის და PascalCase-ების გამოყენებაც დაშვებულია თუ იყენებ BEM მიდგომას(დეტალები [OOCSS და BEM](#oocss-and-bem) სექციაში)
* არ გამოიყენო ID სელექტორები.
* ერთ ინსტრუქციაში რამდენიმე სელექტორის გამოყენების შემთხვევაში თითოეული მათგანი დაწერე ცალკე სტრიქონზე.
* ინსტრუქციის გამოცხადებისას, გამხსნელი ფიგურული ბრჩხილის `}` წინ დასვი გამოტოვება.
* მახასიათებელში, გამოტოვება დასვი ორწერტილის `:` შემდეგ და არა წინ.
* ჩამკეტი ფიგურული ბრჩხილი `}` დასვი ახალ სტრიქონზე.
* ინსტრუქციებს შორის გამოიყენე ცარიელი სტრიქონი.

**ცუდი პრაქტიკა**

```css
.avatar{
    border-radius:50%;
    border:2px solid white; }
.no, .nope, .not_good {
    // ...
}
#lol-no {
  // ...
}
```

**კარგი პრაქტიკა**

```css
.avatar {
  border-radius: 50%;
  border: 2px solid white;
}

.one,
.selector,
.per-line {
  // ...
}
```

### კომენტარები

* უპირატესობა მიანიჭე სტრიქონის კომენტარებს(// Sass-ის გარემოში) და არა ბლოკისას.
* უმჯობესია კომენტარი განათავსო თავის დამოუკიდებელ სტრიქონზე ვიდრე იმავე სტრიქონის ბოლოში სადაც კოდია.
* კოდისთვის რომელიც თვითონ ვერ აღწერს დანიშნულებას დაწერე დეტალური კომენტარი:
  - z-index მახასიათებლის შემთხვევაში
  - ბრაუზერთან თავსებადობის ან მასთან დაკავშირებული სხვა განმარტებისთვის

### OOCSS და BEM

რეკომენდაციას ვუწევთ OOCSS და BEM-ის გარკვეული კომბინაციების გამოყენებას შემდეგი მიზეზების გამო:

  * ისინი გვეხმარება HTML და CSS-ს შორის გასაგები, მკაცრად განსაზღვრული კავშირების შექმნაში
  * ისინი გვეხმარება განმეორებით გამოყენებადი, დამოუკიდებელი კომპონენტების შექმნაში
  * იძლევა ერთმანეთში ნაკლებად ჩალაგებული და ნაკლებად სპეციფიკური კოდის წერის საშუალებას 
  * გვეხმარება მასშტაბირებადი სტილების ცხრილების შექმნაში

**OOCSS**, ანუ ობიექტზე ორიენტირებული CSS, არის მიდგომა რომელიც ხელს გვიწყობს ვიფიქროთ ჩვენი სტილების ცხრილებზე როგორც ობიექტების ერთობლიობაზე, რომლებიც არის ხელახლა გამოყენებადი, განმეორებადი კოდის ამონარიდები რომელთა დამოუკიდებლად გამოყენება შესაძლებელია ვებსაიტის ნებისმიერ ნაწილში.

  * Nicole Sullivan's [OOCSS wiki](https://github.com/stubbornella/oocss/wiki)
  * Smashing Magazine's [OOCSS-ს შესავალი](http://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/)

**BEM** ანუ "ბლოკი-ელემენტი-მოდიფიკატორი" არის HTML და CSS-ში _სახელის განსაზღვრის შეთანხმება_. აღნიშნული მიდგომა შემუშავებული იქნა "იანდექს"-ში კომპლექსური და მასშტაბური აპლიკაციებისთვის და ითვლება როგორც საფუძვლიანი მეთოდოლოგია OOCSS  იმპლემენტაციისთვის. 

  * CSS Trick's [BEM 101](https://css-tricks.com/bem-101/)
  * Harry Roberts' [BEM-ის შესავალი](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)

რეკომენდაციას ვუწევთ BEM-ის და PascalCased ბლოკების სინთეზის ვარიანტს, რომელიც განსაკუთრებულად კარგად მუშაობს კომპონენტებთან(მაგ. რეაქთ) კომბინაციის შემთხვევაში. ქვედა ტირეები და ტირეები კვლავინდებურად გამოიყენება მოდიფიკატორებსა და შვილებთან.

**მაგალითი**

```jsx
// ListingCard.jsx
function ListingCard() {
  return (
    <article class="ListingCard ListingCard--featured">

      <h1 class="ListingCard__title">Adorable 2BR in the sunny Mission.</h1>

      <div class="ListingCard__content">
        <p>Vestibulum id ligula porta felis euismod semper.</p>
      </div>

    </article>
  );
}
```

```css
/* ListingCard.css */
.ListingCard { }
.ListingCard--featured { }
.ListingCard__title { }
.ListingCard__content { }
```

  * `.ListingCard` არის ბლოკი და წარმოადგენს ყველაზე ზედა დონის კომპონენტს
  * `.ListingCard__title` არის ელემენტი და წარმოადგენს `.ListingCard`-ის შთამომავალს რომელიც მონაწილეობს მთლიანი ბლოკის შექმნაში.
  * `.ListingCard--featured` არის მოდიფიკატორი რომელიც წარმოადგენს `.ListingCard` ბლოკის ერთ-ერთ ვარიაციას ან მდგომარეობას.

### ID სელექტორები

მიუხედავად იმისა რომ CSS-ში ელემენტების დასელექთება შესაძლებელია ID-ს მეშვეობით, ეს მიდგომა ზოგადად მიჩნეულია როგორც ცუდი პრაქტიკა. ID სელექტორებს შემოაქვთ ზედმეტად მაღალი დონის [სპეციფიკურობა](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) ინსტრუქციებში და მათი ხელახლა გამოყენება შეუძლებელია.

სპეციფიკურობასთან დაკავშირებით დამატებითი ინფორმაციისთვის წაიკითხეთ [CSS Wizardry-ს სტატის](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/)

### JavaScript hooks

თავი აარიდე ჯავასკრიპტიდან და CSS-დან ერთსა და იმავე კლასზე მიმართვას. აღნიშნული უკეთეს შემთხვევაში იწვევს ზედმეტი დროის ხარჯვას იმ შემთხვევაში თუ საჭირო ხდება კლასის სახელის შეცვლა და შესაბამისად კლასის ყველა ჯვარედინი მითითების პოვნა და შეცვლა, ხოლო უარესში დეველოპერები ხშირად საერთოდ უარს ამბობენ ცვლილებებზე იმის შიშით რომ ფუნქციონალი აირევა.  

რეკომენდირებულია ჯავასკრიპტთან დაკავშირებული კლასების `.js-` პრეფიქსით მონიშვნა:

```html
<button class="btn btn-primary js-request-to-book">ჯავშნის მოთხოვნა</button>
```

### კიდები

იმის მისათითებლად რომ სტილს არ აქვს კიდეები უმჯობესია `0`-ის გამოყენება `none`-ის ნაცვლად.

**ცუდი პრაქტიკა**

```css
.foo {
  border: none;
}
```

**კარგი პრაქტიკა**

```css
.foo {
  border: 0;
}
```
**[⬆ დასაწყისში ასვლა](#table-of-contents)**

## Sass

### სინტაქსი

* გამოიყენე `.scss` გაფართოება და არა ორიგინალი `.sass`
* დაალაგე ნორმალური CSS და `@include` გამოცხადებები ლოგიკურად (დეტალები ქვემოთ)

### მახასიათებლების გამოცხადების თანმიმდევრობა

1. მახასიათებლების გამოცხადება

    გამოაცხადე სტანდარტული მახასიათებლები, ყველაფერი გარდა `@include` ან ჩალაგებული სელექტორებისა.

    ```scss
    .btn-green {
      background: green;
      font-weight: bold;
      // ...
    }
    ```

2. `@include` გამოცხადებები

    `@include` გამოცხადებების დაჯგუფება ბოლოში ამარტივებს მთლიანი სელექტორის წაკითხვას.

    ```scss
    .btn-green {
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);
      // ...
    }
    ```

3. ჩალაგებული სელექტორები

    ჩალაგებული სელექტორები, _აუცილებლოგის შემთხვევაში_, ჩასვი ბოლოში, რის შემდეგაც სრულდება ინსტრუქცია. ყოველი ჩალაგებული სელექტორი ზედა მახასიათებლისგან გამოყოფილი უნდა იყოს ცარიელი სტრიქონით, ასევე რამდენიმე ჩალაგებული სელექტორიც ერთმანეთისგან გამოყავი ცარიელი სტრიქონით. იგივე მიდგომა ვრცელდება შიდა ინსტრუქციებში.

    ```scss
    .btn {
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);

      .icon {
        margin-right: 10px;
      }
    }
    ```

### ცვლადები

უპირატესობა ენიჭება ტირით გამოყოფილ ცვლადის სახელებს(მაგ. `$my-variable`) ვიდრე camelCased ან ქვედა ტირით გამოყოფილებს. ცვლადებისთვის რომლებიც განკუთვნილია მხოლოდ მიმდინარე ფაილში გამოყენებისთვის მიზანშეწონილია ქვედა ტირის პრექისად გამოყენება(მაგ. `$_my-variable`)

### მიქსინები

მიქსინები გამოიყენება DRY პრინციპის იმპლემენტაციის, კოდში სიცხადის შემოტანის და განზოგადებისთვის მსგავსად გონივრულად დასათაურებული ფუნქციებისა. ამ ყველაფრის საშუალებას იძლევა უარგუმენტო მიქსინები, თუმცა გასათვალისწინებელია რომ თუ არ ხდება საბოლოო კოდის შეკუმშვა(მაგ. gzip-ის მეშვეობით) შესაძლებელია მივიღოთ ერთი და იგივე კოდის ზედმეტი გამეორება. 

### Extend მითითება

`@extend`-ის გამოყენება უმჯობესია იყოს თავიდან არიდებული რადგან მისი თვისებები არაინტუიციური და პოტენციურად საშიშია, განსაკუთრებით თუ ისინი გამოყენებულია ჩალაგებულ ინსტრუქციებში. თვით უმაღლეს დონეზე არსებული სელექტორების დაექსთენდებამ შეიძლება გამოიწვიოს გარკვეული პრობლემები თუ სელექტორების თანმიმდევრობა არ არის მუდმივი და შესაძლებელია შეიცვალოს(მაგ. როდესაც ისინი სხვადასხვა ფაილშია და ამ ფაილების ჩატვირთვის თანმიმდევრობა ცვალებადია). Gzip-ის გამოყენებით შესაძლებელია იგივე სარგებლის მიღება რასაც `@extend`-ით მივიღებდით, პლიუს მიქსინებით ვიღებთ უფრო დალაგებულ კოდს, რომელიც იცავს DRY პრინციპს.  

### ჩალაგებული სელექტორები

**არ ჩაალაგო სელექტორები სამზე მეტ დონეზე**

```scss
.page-container {
  .content {
    .profile {
      // STOP!
    }
  }
}
```

როდესაც სელექტორები ხდება ასეთი გრძელი, დიდი ალბათობით წერ კოდს რომელიც:

* მკაცრად დაწყვილებულია HTML-თან (არამყარი) *_ან_*
* ზედმეტად კონკრეტულია (მძლავრი) *_ან_*
* არა ხელმეორედ გამოყენებადია


კიდევ ერთხელ: **არასდრო ჩაალაგო ID სელექტორები!**

If you must use an ID selector in the first place (and you should really try not to), they should never be nested. If you find yourself doing this, you need to revisit your markup, or figure out why such strong specificity is needed. If you are writing well formed HTML and CSS, you should **never** need to do this.
თუ მაინც გიწევს ID სელექტორების გამოყენება(ეცადე რომ თავიდან აირიდო), არასოდეს ჩაალაგო ერთმანეთში. თუ ამჩნევ რომ გიწევს ამის გაკეთება, ჯობია გადახედო HTML სტრუქტურას, ან ეცადო იმის გარკვევას თუ რატომ მოგიწია ასეთი მკაცრი კონკრეტიკის გამოყენება. თუ კარგად დალაგებულ HTML და CSS-ს წერ, **არასდროს** არ უნდა მოგიწიოს ამის გაკეთება.

**[⬆ დასაწყისში ასვლა](#table-of-contents)**

## თარგმანები

  მოცემული სტილისტური სახელმძღვანელო ასევე ხელმისაწვდომია შემდეგ ენებზე:

  - ![id](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Indonesia.png) **Bahasa Indonesia**: [mazipan/css-style-guide](https://github.com/mazipan/css-style-guide)
  - ![tw](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Taiwan.png) **Chinese (Traditional)**: [ArvinH/css-style-guide](https://github.com/ArvinH/css-style-guide)
  - ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Chinese (Simplified)**: [Zhangjd/css-style-guide](https://github.com/Zhangjd/css-style-guide)
  - ![fr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/France.png) **French**: [mat-u/css-style-guide](https://github.com/mat-u/css-style-guide)
  - ![ja](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Japan.png) **Japanese**: [nao215/css-style-guide](https://github.com/nao215/css-style-guide)
  - ![ko](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/South-Korea.png) **Korean**: [CodeMakeBros/css-style-guide](https://github.com/CodeMakeBros/css-style-guide)
  - ![PT-BR](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Brazil.png) **Portuguese (Brazil)**: [felipevolpatto/css-style-guide](https://github.com/felipevolpatto/css-style-guide)
  - ![pt-PT](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Portugal.png) **Portuguese (Portugal)**: [SandroMiguel/airbnb-css-style-guide](https://github.com/SandroMiguel/airbnb-css-style-guide)
  - ![ru](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Russia.png) **Russian**: [rtplv/airbnb-css-ru](https://github.com/rtplv/airbnb-css-ru)
  - ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Spain.png) **Spanish**: [ismamz/guia-de-estilo-css](https://github.com/ismamz/guia-de-estilo-css)
  - ![vn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Vietnam.png) **Vietnamese**: [trungk18/css-style-guide](https://github.com/trungk18/css-style-guide)
  - ![vn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Italy.png) **Italian**: [antoniofull/linee-guida-css](https://github.com/antoniofull/linee-guida-css)
  - ![de](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Germany.png) **German**: [tderflinger/css-styleguide](https://github.com/tderflinger/css-styleguide)

**[⬆ დასაწყისში ასვლა](#table-of-contents)**

## License

(The MIT License)

Copyright (c) 2015 Airbnb

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

**[⬆ back to top](#table-of-contents)**
