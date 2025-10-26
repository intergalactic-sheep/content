🛠 SEO-специалисты советуют соблюдать определённое максимальное количество заголовков, например, использовать:

- `<h2>` — не больше двух, максимум трёх раз;
- `<h3>` — 4-5 раз и так далее.

К сожалению, такой совет часто разбивается о скалы реальности, например, если у вас лендинг с большим количеством секций или секция со множеством карточек:

```html
<body>
  <header class="header">
    <h1 class="header__heading"></h1>
  </header>
  <main class="content">
    <section class="promo">
      <h2 class="promo__heading"></h2>
      ...
    </section>

    <section class="about-company">
      <h2 class="about-company__heading"></h2>
      ...
    </section>

    <section class="teams">
      <h2 class="teams__heading"></h2>
      ...
    </section>

    <section class="why-us">
      <h2 class="why-us__heading"></h2>

      <article class="card">
        <h3 class="card__title"></h3>
      </article>
      <article class="card">
        <h3 class="card__title"></h3>
      </article>
      <article class="card">
        <h3 class="card__title"></h3>
      </article>
      ...
    </section>

    <section class="faq">
      <h2 class="faq__heading"></h2>
      ...
    </section>

    ...
  </main>
</body>
```

Секций и карточек может быть сколько угодно. В попытке ограничить количество заголовков вы навредите семантике и доступности. Поэтому при написании разметки в первую очередь думайте о пользователях, руководствуйтесь здравым смыслом и берите в расчёт контент сайта 😊

🛠 Иногда, в процессе вёрстки можно заметить, что дизайн заголовков повторяется. Допустим, текст сайта имеет такие стили:

```css
body {
  font-size: 18px;
  font-weight: 400;
}

.header__heading {
  font-size: 45px;
  font-weight: 800;
  color: #4A148C;
}

.promo__heading {
  font-size: 31px;
  font-weight: 700;
  color: #2B2B2B;
}

.about-company__heading {
  font-size: 31px;
  font-weight: 700;
  color: #2B2B2B;
}

.why-us__heading {
  font-size: 31px;
  font-weight: 700;
  color: #2B2B2B;
}

.card__title {
  font-size: 20px;
  font-weight: 500;
  color: #000;
}

.footer__heading {
  font-size: 25px;
  font-weight: 300;
  color: #2B2B2B;
}
```

В чем проблема и что сразу бросается в глаза? Большое количество повторяемых стилей. Если вдруг поменяется корпоративный цвет или дизайнер захочет поправить типографику всего сайта — придётся править огромное количество строчек кода. Избежать этого поможет выделение стилей в отдельные _токены_.

**Токены** — свойства, вынесенные в переменные, которые затем можно многократно использовать в любом другом месте в коде. Если какое-то свойство объекта повторяется больше одного раза, стоит задуматься, можно ли его вынести в токен.

Выглядеть токены будут примерно так:

```css
.text-size-3xl {
  font-size: 45px;
}

.text-size-2xl {
  font-size: 31px;
}

.text-size-xl {
  font-size: 25px;
}

.text-size-l {
  font-size: 20px;
}

.text-size-m {
  font-size: 18px;
}

.text-weight-2xl {
  font-weight: 800;
}

.text-weight-xl {
  font-weight: 700;
}

.text-weight-l {
  font-weight: 500;
}

.text-weight-m {
  font-weight: 400;
}

.text-weight-s {
  font-weight: 300;
}

.color-accent {
  color: #4A148C;
}

.color-default {
  color: #000;
}

.color-secondary {
  color: #2B2B2B;
}
```

После того как выделили токены, их можно переиспользовать. Здесь есть на выбор два варианта развития событий.

Прописать классы токенов прямо в разметке:

```html
<body class="text-size-m text-weight-m">
  <header class="header">
    <h1 class="text-size-3xl text-weight-2xl color-accent header__heading"></h1>
  </header>
  <main class="content">
    <section class="promo">
      <h2 class="text-size-2xl text-weight-xl color-secondary promo__heading"></h2>
      ...
    </section>

    <section class="about-company">
      <h2 class="text-size-2xl text-weight-xl color-secondary about-company__heading"></h2>
      ...
    </section>

    <section class="why-us">
      <h2 class="text-size-2xl text-weight-xl color-secondary why-us__heading"></h2>

      <article class="card">
        <h3 class="text-size-l text-weight-l color-default card__title"></h3>
      </article>

      ...
    </section>

    ...
  </main>
  <footer class="footer">
    <h3 class="text-size-xl text-weight-s color-secondary footer__heading"></h3>
  </footer>
</body>
```

Использовать препроцессоры, например, SASS и его директиву `@extend`:

```css
body {
  @extend .text-size-m;
  @extend .text-weight-m;
}

.header__heading {
  @extend .text-size-3xl;
  @extend .text-weight-2xl;
  @extend .color-accent;
}

.promo__heading {
  @extend .text-size-2xl;
  @extend .text-weight-xl;
  @extend .color-secondary;
}

.about-company__heading {
  @extend .text-size-2xl;
  @extend .text-weight-xl;
  @extend .color-secondary;
}

.why-us__heading {
  @extend .text-size-2xl;
  @extend .text-weight-xl;
  @extend .color-secondary;
}

.card__title {
  @extend .text-size-l;
  @extend .text-weight-l;
  @extend .color-default;
}

.footer__heading {
  @extend .text-size-xl;
  @extend .text-weight-s;
  @extend .color-secondary;
}
```
