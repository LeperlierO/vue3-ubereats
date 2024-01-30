<template>
  <div class="restaurant--row">
    <h2 class="title">
        Nos restaurants
    </h2>
    <div class="wrapper--card">
        <router-link class="restaurant--wrapper" v-for="(card, index) in three_restaurant" :key="index" :to="`/restaurant/${card.name}`">
            <restaurant-card :restaurant="card"/>
        </router-link>
    </div>
  </div>
</template>

<script>
import RestaurantCard from './RestaurantCard.vue'
export default {
    name: "RestaurantRow",
    props: {
        three_restaurant: Array
    },
    components: {
        RestaurantCard
    }
}
</script>

<style lang="scss">

    .restaurant--wrapper{
        width: 32%;
        text-decoration: none;
    }

    .restaurant--row {
        .wrapper--card{
            display: flex;
            align-items: center;
            justify-content: space-between;
        }
    }

</style>