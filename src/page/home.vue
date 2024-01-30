<template>
  <div class="home">
    <div class="header">
      <img src="https://d3i4yxtzktqr9n.cloudfront.net/web-eats-v2/ee037401cb5d31b23cf780808ee4ec1f.svg" alt="" srcst=""/>
      <div class="wrapper--input">
        <input type="text" v-model="user_search_restaurant" placeholder="De quoi avez vous envie ?">
        <div class="search">
          <router-link to="/restaurant">
            <div v-for="(restaurant, i) in search_restaurant" :key="i" class="container--restaurant--search">
              <div class="wrapper--img">
                <img :src="restaurant.image" alt="" srcset="">
              </div>
              <p>{{restaurant.name}}</p>
            </div>
          </router-link>
        </div>
      </div>
    </div>
    <div class="banner"></div>
    <restaurant-row v-for="(data, i) in data_restaurant" :key="i" :three_restaurant="data"/>
  </div>
</template>

<script>

// Imports
import BDD from '../bdd.js'
import { onMounted, ref, watch } from 'vue'

// Components
import RestaurantRow from '../components/RestaurantRow.vue'
export default {
  name: 'HomePage',
  components: { RestaurantRow },
  setup() {
    class Restaurant {
      constructor(name, note, image, drive_time) {
        this.name = name
        this.note = note
        this.image = image
        this.drive_time = drive_time
      }
    }

    let data_restaurant = ref([])
    let all_restaurant = []

    const makeDataRestaurant = () => {

      let three_restaurant = []

      for(const restaurant of BDD){
        const resto = new Restaurant(restaurant.name, restaurant.note, restaurant.image, restaurant.drive_time)
        all_restaurant.push(resto)

        three_restaurant.push(resto)

        if(three_restaurant.length == 3){
          data_restaurant.value.push(three_restaurant)
          three_restaurant = []
        }
      }
    }

    // User search restaurant
    let user_search_restaurant = ref('')
    let search_restaurant = ref([])

    watch(user_search_restaurant, (newValue) => {
      let regex = RegExp(newValue.toLowerCase())
      search_restaurant.value = (newValue == "") ? [] : all_restaurant.filter(r => regex.test(r.name.toLowerCase()))
    })

    //
    onMounted(makeDataRestaurant)
      
    return {
      data_restaurant,
      user_search_restaurant,
      search_restaurant
    }
  }
}
</script>

<style lang="scss">

  .home{
    .header {
      height: 120px;
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: space-between;
      img {
        width: 200px;
      }
      .wrapper--input {
        position: relative;
        input {
          background-color: #f6f6f6;
          border: none;
          height: 40px;
          width: 400px;
          outline: none;
          padding-left: 20px;
        }
        .search {
          position: absolute;
          top: 100%;
          width: 100%;
          background-color: #ffffff;

          .container--restaurant--search {
            display: flex;
            align-items: center;
            padding: 10px;

            &:hover {
              background: #f6f6f6;
            }

            .wrapper--img{
              height: 60px;
              width: 60px;
              margin-right: 20px;
              border-radius: 50%;
              overflow: hidden;

              img {
                height: 100%;
                width: auto;
              }
            }
          }
        }
      }
    }
    .banner {
      height: 200px;
      width: 100%;
      background-image: url("https://www.uber-assets.com/image/upload/f_auto,q_auto:eco,c_fill,w_956,h_638/v1622579402/assets/6d/caa1da-ef21-426e-b3be-170af0054fa9/original/WelcomeToUberEats.jpg");
      background-size: cover;
      background-position: center center;
    }
  }

</style>