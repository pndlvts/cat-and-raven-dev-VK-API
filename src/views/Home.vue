<template>
  <section class="home">
    <div class="home__wrapper">
        <swiper class="swiper" :options="swiperOption">
          <swiper-slide v-for="item in slidesText" :key="item.id">
            <div class="swiper-slide__title">
              {{item.title}}
            </div>
            <div class="swiper-slide__text">
              {{item.text}}
              <a class="swiper-slide__btn" v-if="item.button" :href="item.link">
                {{item.button}}
              </a>
            </div>
            <img alt="slide image" :src='item.path'/>
          </swiper-slide>
          <div class="swiper-pagination" slot="pagination"></div>
          <div class="swiper-button-prev" slot="button-prev"></div>
          <div class="swiper-button-next" slot="button-next"></div>
        </swiper>
      <div class="home__container">
        <div class="home__row home__products">
          <h2 class="home__title">Новые товары:</h2>
          <productCard v-for="(product, index) in products.response.items" :key="index"
                       :link='"https://vk.com/cat_and_raven?w=product" + product.owner_id + "_" + product.id + "%2Fquery"'
                       :info="product.description"
                       :image="product.thumb_photo"
                       :prodName="product.title"
                       :price="product.price.text"
                       :productId="product.id"
          >
          </productCard>
        </div>
        <a href="#/products" class="home__button">
          Смотреть все
        </a>
        <a href="#/albums" class="home__button">
          Смотреть подборки
        </a>
        <a href="#/albums" class="home__button">
          Блог
        </a>
      </div>
    </div>
  </section>
</template>

<style lang="scss">
  @import "../assets/styles/helpers/_grid.scss";
  @import "../assets/styles/helpers/_gui.scss";
  .home{
    &__container{
      @include container()
    }
    &__row{
      @include row-flex();
      justify-content: center;
    }
    &__title{
      @include col();
      @include size(12);
      margin-top: 20px;
      margin-bottom: 20px;
      text-align: center;
    }
    &__button{
      background-color: $company;
      color: $white;
      margin-right: auto;
      margin-left: auto;
      padding-top: 20px;
      padding-bottom: 20px;
      width: 400px;
      display: block;
      margin-bottom: 20px;
      text-align: center;
      border-radius: 5px;
      font-size: 20px
    }
  }
  .swiper-pagination-progressbar-fill {
    background: $company !important;
  }

  .swiper-slide {
    width: 100%;
    height: auto;
    max-height: calc(100vh - 75px - 39px);
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
  }

  .swiper-button-next, .swiper-button-prev {
    color: $company !important;
    outline: none;
  }

  .swiper-slide {
    &__btn {
      display: block;
      width: 270px;
      text-align: center;
      padding-top: 20px;
      padding-bottom: 20px;
      border-radius: 5px;
      background-color: $white;
      color: $black;
      text-shadow: none;
      margin-top: 10px;
      box-shadow: 0 0 25px $black;
      transition: .2s;
    }

    &__btn:hover {
      background-color: rgba($company, .9);
      transition: .2s;
    }

    &__title {
      position: absolute;
      left: 10%;
      top: 20%;
      color: $white;
      font-size: 2rem;
      text-shadow: 1px 1px 1px $black;
      border: none;
      border-top: 2px solid $white;
    }

    &__text {
      position: absolute;
      left: 10%;
      top: calc(20% + 40px);
      max-width: 60%;
      color: $white;
      font-size: 1rem;
      text-shadow: 1px 1px 1px $black;
    }

    img {
      width: 100%;
      height: auto;
    }
  }

  @include to-sm() {
    .home{
      &__button{
        width: 100%;
      }
    }
    .swiper-slide {
      max-height: calc(100vh - 75px);
    }
    .swiper-button-next, .swiper-button-prev {
      display: none;
    }
    .swiper-slide {
      &__btn {
        max-width: 150px;
        padding-top: 10px;
        padding-bottom: 10px;
        margin-top: 10px;
      }

      &__btn:hover {
        background-color: $white;;
      }

      &__title {
        position: absolute;
        left: 5%;
        top: 10%;
        color: $white;
        font-size: 1rem;
        text-shadow: 1px 1px 1px $black;
        border: none;
        border-top: 1px solid $white;
        max-width: 90%;
      }

      &__text {
        position: absolute;
        left: 5%;
        top: calc(10% + 20px);
        max-width: 100%;
        color: $white;
        font-size: .7rem;
      }
    }
  }
</style>

<script>
import { Swiper, SwiperSlide } from 'vue-awesome-swiper'
import 'swiper/css/swiper.css'
import slidesText from '../../public/media/forHomeSlider/textForSlides/textForSlides'
import axios from 'axios-jsonp-pro'
import productCard from '../components/product-card'

export default {
  name: 'Home',
  components: {
    Swiper,
    SwiperSlide,
    productCard
  },
  data () {
    return {
      swiperOption: {
        pagination: {
          el: '.swiper-pagination',
          type: 'progressbar'
        },
        navigation: {
          nextEl: '.swiper-button-next',
          prevEl: '.swiper-button-prev'
        },
        autoplay: {
          delay: 5000
        },
        loop: true
      },
      slidesText: slidesText,
      products: null
    }
  },
  mounted () {
    axios.jsonp('https://api.vk.com/method/market.get?owner_id=-153796975&access_token=d42e0cf2def9f4942c5b1093b036eefe721c46bc95da644241946b5c33c8831e4d49d50703541572e2a0c&count=3&v=5.59')
      .then(response => (this.products = response))
      .catch(function (error) {
        console.log(error)
      })
  }
}
</script>
