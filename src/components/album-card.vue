<template lang="pug">
  include ../../node_modules/bempug/index
  - BEMPUG.modifier = '_';
  - BEMPUG.element = '__';
  +b("card")
    +e("image", { t: "img" })(:src="image")
    +e("footer")
      +e("link", { t: "a" })(:href="link" v-html='albName')
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
    @include size-hd(5);
    @include size-xl(5);
    @include size-lg(5);
    @include size-md(4);
    @include size-sm(4);
    @include size-xs(12);
    margin-bottom: 20px;
    position: relative;

    &__image {
      width: 100%;
      height: auto;
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
  name: 'albumCard',
  props: {
    info: String,
    image: String,
    albName: String,
    price: String,
    link: String,
    albumId: Number
  }
}
</script>
