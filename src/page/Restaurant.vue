<template>
  <router-link to="/" style="text-decoration:none">
    <div id="return">Home</div>
  </router-link>

  <div>
    <img :src="restaurant.image" alt="">
  </div>
  <p>{{ restaurant.name }}</p>
  <p>Note {{ restaurant.note }}</p>
  <p>Livraison {{ restaurant.drive_time }}</p>
</template>

<script>
import BDD from '../bdd'
import { useRoute } from 'vue-router'
export default {
    name: 'RestaurantPage',
    setup() {

      const route = useRoute()
      const restaurant = BDD.find((restaurant) => restaurant.name === route.params.name)

      return {
        restaurant
      }
      
    }
}
</script>

<style lang="scss" scoped>
  #return{
    margin: 25px 45px;
    font-weight: 400;
    
    &:hover {
      font-weight: 900;
    }
  }
</style>