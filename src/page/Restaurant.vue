<template>
  <RouterLink to="/">
    <div id="return">< Retour à la home</div>
  </RouterLink>
  <div>
    <img :src="restaurant.image" :alt="restaurant.name" />
  </div>
  <p>{{ restaurant.name }}</p>
  <p>Note: {{ restaurant.note }}</p>
  <p>Temps de livraison: {{ restaurant.drive_time }}</p>
</template>

<script>
import BDD from '../bdd';
import { onMounted } from 'vue';
import { useRoute } from 'vue-router';

export default {
  name: 'Restaurant',
  setup() {
    const route = useRoute();

    const restaurant = BDD.find(
      (restaurant) => restaurant.name === route.params.name
    );

    onMounted(() => {
      console.log('route:', route.params.name);
    });

    return {
      restaurant,
    };
  },
};
</script>

<style lang="scss" scoped>
/*CSS */
#return {
  margin: 25px 45px;
  font-weight: 900;
  text-decoration: none;
  color: #000;

  &:hover {
    font-weight: bold;
    cursor: pointer;
  }
}
</style>
