<template lang="pug">
  <!-- bembug -->
  include ../node_modules/bempug/index
  - BEMPUG.modifier = '_';
  - BEMPUG.element = '__';
  <!-- bembug -->
  #app
    +b("header", {t: "header"})
      +e("wrapper-top")
        +e("container")
          +e("row")
            +e("top")
              +e("top-left")
                a(href="/#/")
                  +e("logo", {t: "img src=./assets/media/logo.png alt=' ' title='Кот и Ворон'"})
                router-link(class="header__btn" to="/") Главная
                +e("btn", {t: "button"})(data-position="footer" @click="showFooter") Контакты
              +e("top-right")
                span Режим работы: по воскресеньям с
                  span.time  13:00
                  |  до
                  span.time  18:00
              +b("hamburger")(@click='toggleHamburger')
                +e("bar")
                +e("bar")
                +e("bar")
      +e("wrapper-bottom")
        +e("container")
          +e("row")
            +e("main-menu")
              +e("nav", {t:"nav"})
                router-link(class="header__link" to="/products") Товары
                router-link(class="header__link" to="/albums") Подборки
                router-link(class="header__link" to="/reviews") Блог
              +e("help")
                +e("help-btn", {t: "button"})(@click="showContentError") Я не вижу контент
    router-view
    footerComp
    +b("content-err")
      +e("wrapper")
        +e("container")
          +e("info") Наш веб-ресурс получает информацию при помощи VK API. Возможно, Ваш браузер блокирует контент. Если Вы используете режим инкогнито, пожалуйста, отключите его или используйте другой веб-браузер.
</template>

<style lang="scss">
  @import "assets/styles/main";
  #app{
    font-family: 'PT Sans';
    background-color: $white;
  }
  .header{
    &__wrapper-top, &__wrapper-bottom{
      width: 100%;
      background-color: $white;
    }
    &__wrapper-top, &__wrapper-bottom{
      border-bottom: 1px solid $gray;
    }
    &__container{
      @include container();
    }
    &__row{
      @include row-flex;
      align-items: center;
    }
    &__top{
      @include col();
      @include size(12);
      display: flex;
      justify-content: space-between;
    }
    &__top-left, &__top-right{
      display: flex;
      align-items: center;
    }
    &__btn, &__btn:active, &__btn:visited{
      color: $gray2;
      font-size: 14px;
      border: none;
      border-radius: 3px;
      background: none;
      padding: 8px;
      cursor: pointer;
      transition: .3s;
      text-transform: uppercase;
    }
    &__btn:hover{
      color: $company;
      transition: .3s;
    }
    &__main-menu{
      display: flex;
      justify-content: space-between;
      width: 100%;
    }
    &__nav{
      @include col();
      @include size(9);
    }
    &__logo{
      width: auto;
      height: 50px;
      width: auto;
      padding-top: 10px;
      padding-bottom: 10px;
      margin-right: 10px;
    }
    &__link, &__link:active, &__link:visited{
      display: inline-block;
      color: $black;
      font-size: 14px;
      padding-top: 10px;
      padding-bottom: 10px;
      margin-left: 25px;
      font-weight: normal;
      transition: .3s;
    }
    &__link:hover{
      color: $company;
      transition: .3s;
    }
    &__link:first-child{
      margin-left: 0;
    }
    &__help{
      @include col();
      @include size(3);
      display: flex;
      justify-content: flex-end;
    }
    &__help-btn{
      cursor: pointer;
      color: crimson;
      border: none;
      background: none;
      height: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 16px;
    }
  }
  .time{
    color: $company
  }
  .hamburger{
    display: none;
  }
  .content-err{
    opacity: 0;
    transition: .5s;
    position: absolute;
    z-index: -1;
    top: 0;
    left: 0;
    width: 100%;
    color: #fff;
    &__container{
      @include container();
      background: crimson;
      border-bottom-left-radius: 5px;
      border-bottom-right-radius: 5px;
    }
  }
  .content-err_show{
    opacity: 1;
    z-index: 999;
    transition: .5s;
  }
  @include to-sm(){
    .header{
      &__main-menu{
        display: block;
        overflow: visible;
      }
      &__nav{
        @include size(12)
      }
      &__help{
        position: relative;
        @include size(12);
        justify-content: flex-start;
        margin-bottom: 15px;
        padding-top: 15px;
      }
      &__help::before{
        content: " ";
        display: block;
        height: 1px;
        width: calc(100% + 40px);
        background-color: $gray;
        position: absolute;
        top: 0;
        left: -20px;
      }
      &__help-btn{
        font-size: 12px;
        display: flex;
        justify-content: flex-start;
        width: 100%;
      }
      &__btn{
        font-size: 12px;
      }
      &__nav{
        display: block;
      }
      &__top{
        align-items: center;
      }
      &__top-right{
        display: none;
      }
      &__wrapper-bottom{
        max-height: 0;
        overflow: hidden;
        transition: .5s;
        border-bottom: 0;
      }
      &__wrapper-bottom_active{
        max-height: 100vh;
        transition: .5s;
        border-bottom: 1px solid $gray;
      }
      &__link, &__link:active, &__link:visited{
        display: block;
        margin-left: 0;
      }
    }
    .hamburger{
      display: block;
      width: 5px;
      height: 20px;
      position: relative;
      cursor: pointer;
      padding: 5px;
      border: none;
      border-radius: 50%;
      transition: .5s;
      transition-delay: 0s;
      &__bar{
        display: block;
        height: 2px;
        background-color: $gray2;
        position: absolute;
        width: 100%;
        border-radius: 20px;
      }
      &__bar:nth-child(1){
        top: 9px;
        left: 0;
        transition: transform .2s linear .7s, top .2s linear .5s;
      }
      &__bar:nth-child(2){
        top: 14px;
        left: 0;
        transition: .5s;
        opacity: 1;
      }
      &__bar:nth-child(3){
        bottom: 9px;
        left: 0;
        transition: bottom .2s linear .5s, transform .2s linear .7s;
      }
    }
    .hamburger_active{
      border: none;
      transform: rotate(45deg);
      transition: .5s;
      transition-delay: 1s;
      .hamburger__bar{
        background-color: $company;
        width: 100%;
        border-radius: 0;
      }
      .hamburger__bar:nth-child(1){
        transform: rotate(90deg);
        top: 14px;
        left: 0;
        transition: top .2s linear 0s, transform .2s linear .5s;
      }
      .hamburger__bar:nth-child(2){
        opacity: 0;
        transition: .5s;
      }
      .hamburger__bar:nth-child(3){
        transform: rotate(0deg);
        bottom: 14px;
        left: 0;
        transition: bottom .2s linear 0s, transform .2s linear .2s;
      }
    }
  }
</style>

<script>
import footerComp from './components/footer'

export default {
  name: 'app',
  components: {
    footerComp
  },
  methods: {
    toggleHamburger: function () {
      document.querySelector('.hamburger').classList.toggle('hamburger_active')
      document.querySelector('.header__wrapper-bottom').classList.toggle('header__wrapper-bottom_active')
    },
    closeMobileMenu: function () {
      document.querySelector('.hamburger').classList.remove('hamburger_active')
      document.querySelector('.header__wrapper-bottom').classList.remove('header__wrapper-bottom_active')
    },
    showFooter: function () {
      document.querySelector('footer').scrollIntoView({ behavior: 'smooth' })
    },
    showContentError: function () {
      document.querySelector('.content-err').classList.add('content-err_show')
      setTimeout(() => { document.querySelector('.content-err').classList.remove('content-err_show') }, 4000)
    }
  }
}
</script>
