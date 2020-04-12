<template>
  <section class="albums">
    <div class="albums__wrapper">
      <div class="albums__container">
        <div class="albums__row">
           <albumCard v-for="(album, index) in albums.response.items" :key="index"
                       :link='"https://vk.com/market-153796975?section=album_" + album.id'
                       :image="album.photo.photo_604"
                       :albName="album.title"
          >
          </albumCard>
        </div>
      </div>
    </div>
  </section>
</template>

<style lang="scss">
  @import "../assets/styles/helpers/_grid.scss";
  @import "../assets/styles/helpers/_gui.scss";
  .albums{
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
    .albums{
      &__row{
        padding-left: 90px;
      }
    }
  }
  @include to-sm(){
    .albums {
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
import albumCard from '../components/album-card'

export default {
  name: 'albums',
  components: {
    albumCard
  },
  data () {
    return {
      albums: {},
      more: null,
      amount: null,
      counter: 20 // т.к. первые 10 и more в подгрузке
    }
  },
  methods: {
  },
  mounted () {
    axios.jsonp('https://api.vk.com/method/market.getAlbums?owner_id=-153796975&access_token=d42e0cf2def9f4942c5b1093b036eefe721c46bc95da644241946b5c33c8831e4d49d50703541572e2a0c&count=100&v=5.59')
      .then(response => (this.albums = response))
      .catch(function (error) {
        console.log(error)
      })
  }
}
</script>
