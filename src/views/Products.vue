<template>
  <section class="products">
    <div class="products__wrapper">
      <div class="products__container">
        <div class="products__row">
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
        <button class="products__showMore" @click="showMore()">Показать еще</button>
      </div>
    </div>
  </section>
</template>

<style lang="scss">
  @import "../assets/styles/helpers/_grid.scss";
  @import "../assets/styles/helpers/_gui.scss";
  .products{
    &__wrapper{
      min-height: calc(100vh - 75.5px - 38.5px);
    }
    &__container{
      @include container();
      min-height: calc(100vh - 75.5px - 38.5px);
    }
    &__row{
      @include row-flex();
      align-self: stretch;
      padding-top: 20px;
      padding-bottom: 20px;
      padding-left: 150px;
    }
    &__showMore{
      margin-bottom: 40px;
      width: 398px;
      margin-left: auto;
      margin-right: auto;
      background-color: $company;
      border: 1px solid $company;
      border-radius: 5px;
      text-align: center;
      font-size: 20px;
      padding-top: 19px;
      padding-bottom: 19px;
      color: $white;
      transition: .5s;
      cursor: pointer;
      display: block;
    }
    &__showMore:hover{
      transition: .5s;
      border: 1px solid $company;
      background-color: $white;
      color: $company;
    }
  }
  @include to-md(){
    .products{
      &__row{
        padding-left: 90px;
      }
    }
  }
  @include to-sm(){
    .products {
      min-height: calc(100vh - 75.5px);
      &__row{
        padding-left: 0;
      }
      &__showMore{
        width: 100%;
      }
    }
  }
</style>

<script>
import axios from 'axios-jsonp-pro'
import productCard from '../components/product-card'

export default {
  name: 'Products',
  components: {
    productCard
  },
  data () {
    return {
      products: null,
      more: null,
      amount: null,
      counter: 20 // т.к. первые 10 и more в подгрузке
    }
  },
  methods: {
    showMore: function () {
      this.amount = this.products.response.count
      for (const item of this.more.response.items) {
        document.querySelector('.products__row').innerHTML += '<div class="card">' +
          '<button class="card__info-btn" data-info="' + item.id + '"></button>' +
          '<div class="card__info-block" data-game="' + item.id + '">' +
            '<div class="card__title">' + item.title + '</div>' +
            '<div class="card__info">' + item.description + '</div>' +
          '</div>' +
          '<img class="card__image" src="' + item.thumb_photo + '"/>' +
          '<div class="card__footer">' +
            '<a class="card__link" href="' + 'https://vk.com/cat_and_raven?w=product' + item.owner_id +
          '_' + item.id + '%2Fquery' + '">Купить за <span>' + item.price.text + '</span></a>' +
          '</div>'
        this.counter++
      }
      if (this.counter >= this.amount - 1) {
        document.querySelector('.products__showMore').style.display = 'none'
      }
      document.querySelectorAll('.card__info-btn').forEach(
        infoBtn => {
          infoBtn.addEventListener('click', () => {
            infoBtn.classList.toggle('card__info-btn_active')
            const infoBlock = document.querySelector('[data-game="' + infoBtn.dataset.info + '"]')
            infoBlock.classList.toggle('card__info-block_active')
          })
        }
      )
      axios.jsonp('https://api.vk.com/method/market.get?owner_id=-153796975&access_token=d42e0cf2def9f4942c5b1093b036eefe721c46bc95da644241946b5c33c8831e4d49d50703541572e2a0c&count=10&offset=' + this.counter + '&v=5.59')
        .then(response => (this.more = response))
        .catch(function (error) {
          console.log(error)
        })
    }
  },
  mounted () {
    axios.jsonp('https://api.vk.com/method/market.get?owner_id=-153796975&access_token=d42e0cf2def9f4942c5b1093b036eefe721c46bc95da644241946b5c33c8831e4d49d50703541572e2a0c&count=10&v=5.59')
      .then(response => (this.products = response))
      .catch(function (error) {
        console.log(error)
      })
    axios.jsonp('https://api.vk.com/method/market.get?owner_id=-153796975&access_token=d42e0cf2def9f4942c5b1093b036eefe721c46bc95da644241946b5c33c8831e4d49d50703541572e2a0c&count=10&offset=10&v=5.59')
      .then(response => (this.more = response))
      .catch(function (error) {
        console.log(error)
      })
  }
}
</script>
