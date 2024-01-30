<template>
  <div class="restaurant--card">
    <div :style="changeBackground()" class="restaurant--image">

    </div>
    <div class="restaurant--informations">
      <div class="top">
        <p class="name">
          {{ restaurant.name }}
        </p>
        <p class="note">
          <span>
            {{ restaurant.note }}
          </span>
        </p>
      </div>
      <p class="tme">
        {{ restaurant.drive_time }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "RestaurantCard",
  props: {
    restaurant: Object
  },
  setup(props) {
    const changeBackground = () => {
      return {
        backgroundImage: `url(${props.restaurant.image})`
      }
    }

    return {
      changeBackground
    }
  }
}
</script>

<style lang="scss">
    .restaurant--card { 
        width: 32%;
        height: 30vh;

        p {
          margin: 0px;
        }

        .restaurant--image{
          height: 70%;
          border-radius: 15px;
          background-size: cover;
          background-position: center;
        }

        .restaurant--informations{
          
          .top {
            margin: 10px 0;
            display: flex;
            align-items: center;
            justify-content: space-between;

            .note {
              background-color: #eeeeee;
              height: 30px;
              width: 30px;
              display: flex;
              align-items: center;
              justify-content: center;
              font-size: 0.8rem;
              border-radius: 50%;
            }
          }

          .time {
            font-size: 0.9rem;
          }
        }
    }

</style>