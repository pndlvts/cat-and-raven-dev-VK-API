<template lang="pug">
  <!-- bembug -->
  include ../../node_modules/bempug/index
  - BEMPUG.modifier = '_';
  - BEMPUG.element = '__';
  <!-- bembug -->
  +b("footer", {t:"footer"})
    +e("wrapper")
      +e("container")
        +e("row")
          +e("small-block")
            +e("title", {t: "h3"})(data-title='menu' @click='openFooterMenu') Меню
            +e("data-block")(data-anchor='menu')
              +e("nav", {t: nav})
                router-link(class="footer__link" to="/") Главная
                router-link(class="footer__link" to="/products") Товары
                router-link(class="footer__link" to="/albums") Подборки
                router-link(class="footer__link" to="/reviews") Блог
                router-link(class="footer__link" to="/help") Помощь
          +e("block")
              +e("title", {t: "h3"})(data-title='social' @click='openFooterMenu') Давайте дружить
              +e("data-block")(data-anchor='social')
                +e("sub-title", {t: "p"}) Присоединяйтесь к нам в социальных сетях и всегда будьте в курсе событий.
                +e("social-icons")
                  +e("social-icon vk", {t: "a href=https://vk.com/cat_and_raven"})
                  +e("social-icon inst", {t: "a href=https://www.instagram.com/cat_and_raven/"})
          +e("block")
            +e("logo", {t:"img src=../assets/media/logo.svg alt=' ' title='Кот и Ворон'"})
        +e("row")
          +e("info")
            +e("title", {t: "h3"})(data-title='contacts' @click='openFooterMenu') Контакты
            +e("data-block")(data-anchor='contacts')
              +e("addr") Восточный переулок, 42, Геленджик
              +e("creator", {t: "a href='tel:89881371167'"}) +7 (988) 137-11-67
              +e("creator", {t: "a href='mailto:cat_and_raven@mail.ru'"}) cat_and_raven@mail.ru
          +e("map")
            div(style="position:relative;overflow:hidden;")
              a(href="https://yandex.ru/maps/10990/gelendgik/?utm_medium=mapframe&utm_source=maps" style="color:#eee;font-size:12px;position:absolute;top:0px;") Геленджик
              a(href="https://yandex.ru/maps/10990/gelendgik/house/vostochny_pereulok_42/Z0EYdg5jT0MGQFpufXl3cX9mYw==/?ll=38.093662%2C44.560357&sll=38.975313%2C45.035470&sspn=0.136642%2C0.063292&utm_medium=mapframe&utm_source=maps&z=16" style="color:#eee;font-size:12px;position:absolute;top:14px;") Восточный переулок, 42 — Яндекс.Карты
              iframe(src="https://yandex.ru/map-widget/v1/-/CKq3u62-" allowfullscreen="true" style="position:relative;")
        +e("row-copy")
          +e("creator-copy", {t: "a href=https://vk.com/in_tenebris_lumen"}) Иван Нагих – основатель проекта
          +e("creator-copy", {t: "a href=https://vk.com/pndlvts"}) Панделов Тимофей – создание сайта
          +e("copyright") © 2017 – 2020 Кот и Ворон

</template>

<style lang="scss">
  @import "../assets/styles/helpers/_grid";
  @import "../assets/styles/helpers/_gui";
  .footer{
    &__wrapper{
      border-top: 1px solid $gray;
      background-color: $white;
      padding-bottom: 80px;
      padding-top: 80px;
    }
    &__container{
      @include container();
    }
    &__row{
      @include row-flex();
      justify-content: space-between;
    }
    &__block{
      @include col();
      @include size-hd(4);
      @include size-xl(4);
      @include size-lg(4);
      @include size-md(4);
      @include size-sm(4);
      @include size-xs(12);
      position: relative;
    }
    &__small-block{
      @include col();
      @include size-hd(2);
      @include size-xl(2);
      @include size-lg(2);
      @include size-md(2);
      @include size-sm(2);
      @include size-xs(12);
    }
    &__title{
      margin-bottom: 20px;
      font-size: 20px;
      cursor: pointer;
    }
    &__title:after{
      content: " ";
      display: inline-block;
      right: 0;
      height: 15px; width: 15px;
      border: 1px solid $company;
      border-width: 2px 2px 0 0;
      transition: .5s;
      border-top-right-radius: 2px;
      margin-left: -5px;
    }
    &__link, &__link:active, &__link:visited, &__link:hover{
      display: block;
      color: $gray2;
      margin-bottom: 10px;
      font-size: 20px;
    }
    &__sub-title{
      font-size: 12px;
      color: $gray2;
      width: 70%;
    }
    &__social-icons{
      position: absolute;
      bottom: 0;
    }
    &__social-icon{
      display: inline-block;
      height: 48px;
      width: 48px;
      margin-left: 10px;
      border-radius: 10px;
    }
    &__social-icon:first-child{
      margin-left: 0;
    }
    .vk{
      background-image: url('../assets/sprites/social.png');
      background-position: -78px -10px;
      background-repeat: no-repeat;
      transition: .3s;
    }
    .vk:hover{
      background-position: -10px -10px;
      transition: .3s;
    }
    .inst{
      background-image: url('../assets/sprites/social.png');
      background-position: -78px -78px;
      background-repeat: no-repeat;
      transition: .3s;
    }
    .inst:hover{
      background-position: -10px -78px;
      transition: .3s;
    }
    &__logo{
      height: 200px;
      width: auto;
      margin-left: calc(100% - 200px);
    }
    &__info{
      @include col();
      @include size(5);
      @include size-xs(12);
      margin-top: 40px;
    }
    &__map{
      @include col();
      @include size(5);
      @include size-xs(12);
      margin-top: 40px;
    }
    iframe{
      width: 100%;
      border: none;
      border-radius: 5px;
    }
    &__creator, &__creator:visited, &__creator:active, &__creator:hover{
      color: $black;
      display: block;
    }
    &__row-copy{
      @include row-flex;
      margin-top: 40px;
    }
    &__creator-copy, &__creator-copy:active, &__creator-copy:visited, &__creator-copy:hover{
      color: $black;
      display: block;
      @include col();
      @include size(12);
    }
    &__copyright{
      @include col();
      @include size(12);
    }
  }
  @include to-lg(){
    .footer{
      &__social-icons{
        position: static;
        margin-top: 10px;
      }
      &__logo{display: none}
      .vk{
        background-position: -10px -10px;
      }
      .inst{
        background-position: -10px -78px;
      }
    }
  }
  @include to-sm(){
    .footer{
      padding-bottom: 30px;
      &__title{
        transition: .5s;
        position: relative;
        margin-bottom: 15px;
      }
      &__title_active{
        color: $company;
        transition: .5s;
      }
      &__title:after{
        position: absolute;
        right: 0;
        transform: rotate(135deg);
      }
      &__title_active:after{
        transform: rotate(0deg);
        width: 20px;
        height: 20px;
        transition: transform .2s linear 0s, width .2s linear .5s, height .2s linear .5s;
      }
      &__data-block{
        overflow: hidden;
        max-height: 0;
        transition: .5s;
      }
      &__data-block_active{
        max-height: 100%;
        transition: .5s;
      }
      &__logo{
        display: none;
      }
      &__info{
        margin-top: 0;
      }
    }
  }
</style>

<script>
export default {
  name: 'footerComp',
  methods: {
    openFooterMenu: (event) => {
      const el = event.target
      const data = el.dataset.title
      const anchor = document.querySelector('[data-anchor="' + data + '"]')
      el.classList.toggle('footer__title_active')
      anchor.classList.toggle('footer__data-block_active')
    }
  }
}
</script>
