<template>
  <div class="restaurant--row">
    <h2 class="title">Nos restaurants</h2>
    <div class="wrapper--card">
      <RouterLink
        class="restaurant--wrapper"
        v-for="(restaurant, index) in threerestaurants"
        :key="index"
        :to="{ name: 'Restaurant', params: { name: restaurant.name } }"
      >
        <RestaurantCard :inforestaurant="restaurant" />
      </RouterLink>
    </div>
  </div>
</template>

<script>
import RestaurantCard from './RestaurantCard.vue';

export default {
  name: 'RestaurantRow',
  components: {
    RestaurantCard,
  },
  props: {
    threerestaurants: Array,
  },
};
</script>

<style lang="scss">
/* CSS / SCSS */
.restaurant--row {
  .restaurant--wrapper {
    width: 32%;
    text-decoration: none;
    color: #000;
    &:hover {
      cursor: pointer;
      font-weight: 900;

      .restaurant--image {
        opacity: 50%;
      }
    }
  }
  .wrapper--card {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
}
</style>
