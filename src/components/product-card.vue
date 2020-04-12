<template lang="pug">
  include ../../node_modules/bempug/index
  - BEMPUG.modifier = '_';
  - BEMPUG.element = '__';
  +b("card")
    +e("info-btn", { t: 'button' })(:data-info="productId" @click="showDescription")
    +e("info-block")(:data-game="productId")
      +e("title")(v-html='"<span>Наименование: </span>" + prodName')
      +e("info")(v-html="\"<span>Описание: </span>\" + info")
    +e("image", { t: "img" })(:src="image")
    +e("price")
    +e("footer")
      +e("link", { t: "a" })(:href="link" v-html='"Купить за <span>" + price + "</span>"')
</template>

<style lang="scss">
  @import "../assets/styles/helpers/_grid";
  @import "../assets/styles/helpers/_gui";

  .card {
    background: none;
    border: 1px solid $gray;
    border-radius: 3px;
    overflow: hidden;
    transition: .5s;
    @include col();
    @include size-hd(3);
    @include size-xl(3);
    @include size-lg(3);
    @include size-md(4);
    @include size-sm(4);
    @include size-xs(12);
    margin-bottom: 20px;
    position: relative;
    &__info-block{
      position: absolute;
      width: 100%;
      height: calc(100% - 52px);
      overflow: hidden;
      transition: .5s;
      background-color: $white;
      z-index: -1;
      opacity: 0;
    }
    &__info-block_active{
      transition: .5s;
      z-index: 2;
      overflow-y: scroll;
      opacity: 1;
    }
    &__info-btn{
      z-index: 3;
      outline: none;
      background-color: $company;
      border: none;
      color: $black;
      height: 50px;
      width: 50px;
      position: absolute;
      right: -10px;
      top: -10px;
      border-radius: 50%;
      cursor: pointer;
      transition: .5s;
    }
    &__info-btn:hover{
      transform: scale(1.2);
      transition: .5s;
    }
    &__info-btn::before{
      content: "i";
      left: 50%;
      top: 50%;
      color: $black
    }
    &__info-btn_active{
      background-color: rgba($company, .8);
    }
    &__info-btn_active::before{
      content: "x";
      left: 50%;
      top: 50%;
      color: $black
    }
    &__title, &__info{
      text-align: justify;
      padding: 10px;
      span{
        font-weight: bold;
      }
    }
    &__image {
      width: 100%;
      height: auto;
    }

    &__price{
      margin-bottom: 45px;
      color: $company
    }
    &__footer {
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      min-height: 20px;
      border-top: 1px solid $gray3;
      background-color: $gray;
    }
    &__link, &__link:active, &__link:visited{
      text-transform: uppercase;
      font-size: 16px;
      display: block;
      padding: 15px;
      text-decoration: none;
      color: $black;
      position: relative;
      span{
        color: $company;
      }
    }
    &__link::after{
      content: " ";
      display: block;
      border: none;
      height: 9px;
      width: 9px;
      border-top: 1px solid $black;
      border-right: 1px solid $black;
      background: none;
      position: absolute;
      right: 10px;
      top: 20px;
      transform: rotate(45deg);
    }
  }
  .card:hover {
    box-shadow: 0px 0px 5px $company;
    transition: .5s;
  }
</style>

<script>
export default {
  name: 'productCard',
  props: {
    info: String,
    image: String,
    prodName: String,
    price: String,
    link: String,
    productId: Number
  },
  methods: {
    showDescription: (event) => {
      const btnData = event.target.dataset.info
      const descriptionBlock = document.querySelector('[data-game="' + btnData + '"]')
      descriptionBlock.classList.toggle('card__info-block_active')
      event.target.classList.toggle('card__info-btn_active')
    }
  }
}
</script>
