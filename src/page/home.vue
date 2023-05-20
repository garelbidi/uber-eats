<template>
  <div id="home">
    <div class="header">
      <img
        src="https://d3i4yxtzktqr9n.cloudfront.net/web-eats-v2/ee037401cb5d31b23cf780808ee4ec1f.svg"
        alt="Uber Eats"
      />
      <div class="wrapper--input">
        <input
          v-model="user_search_restaurant"
          type="text"
          placeholder="De quoi avez-vous envie ?"
        />
          <router-link v-for="(resto, i) in search_restaurant"
            :key="i" :to="{name: 'Restaurant', params:{name: resto.name}}">
            <div class="search">
              <div  class="container--restaurant--search">
                <div class="wrapper--img">
                  <img :src="resto.image" :alt="resto.name" />
                </div>
                <p>{{ resto.name }}</p>
              </div>
            </router-link>

          </div>
      </div>
    </div>

    <div class="banniere"></div>

    <RestaurantRow
      v-for="(data, i) in datarestaurant"
      :key="i"
      :threerestaurants="data"
    />
  </div>
</template>

<script>
import RestaurantRow from '../components/RestaurantRow';
import BDD from '../bdd';
import { onMounted, ref, watch } from 'vue';

export default {
  name: 'Home',
  components: {
    RestaurantRow,
  },
  setup() {
    //console.log(BDD);
    class Restaurant {
      constructor(name, note, image, drive_time) {
        this.name = name;
        this.note = note;
        this.image = image;
        this.drive_time = drive_time;
      }
    }

    // Tableau qui regroupe les restos par lignes de 3 !
    let datarestaurant = ref([]);
    let allrestaurants = [];

    const makeDataRestaurant = () => {
      let threerestaurants = [];

      for (const restaurant of BDD) {
        const new_restaurant = new Restaurant(
          restaurant.name,
          restaurant.note,
          restaurant.image,
          restaurant.drive_time
        );

        // tableau all restaurants pour stocker
        allrestaurants.push(new_restaurant);

        if (threerestaurants.length === 2) {
          threerestaurants.push(new_restaurant);
          datarestaurant.value.push(threerestaurants);
          threerestaurants = [];
        } else {
          threerestaurants.push(new_restaurant);
        }
      }
    };

    //User search restaurant
    let user_search_restaurant = ref('');
    let search_restaurant = ref([]);

    watch(user_search_restaurant, (new_value) => {
      //console.log(new_value, allrestaurants);
      let regex = RegExp(new_value.toLowerCase());

      let new_search_restaurant = allrestaurants.filter((restaurant) =>
        regex.test(restaurant.name.toLowerCase())
      );

      new_value == 0
        ? (search_restaurant.value = [])
        : (search_restaurant.value = new_search_restaurant);

      console.log(new_value);
    });

    onMounted(makeDataRestaurant);

    return {
      datarestaurant,
      user_search_restaurant,
      search_restaurant,
    };
  },
};
</script>

<style lang="scss">
/* CSS / SCSS */
.header {
  height: 120px;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

img {
  width: 200px;
}

input {
  background-color: #f6f6f6;
  width: 400px;
  height: 60px;
  outline: none;
  border: none;
  padding-left: 20px;
}

.banniere {
  height: 200px;
  width: 100%;
  background-image: url('https://www.lsa-conso.fr/mediatheque/6/9/7/000492796_896x598_c.png');
  background-size: cover;
  background-position: center center;
}

.wrapper--input {
  position: relative;

  .search {
    position: absolute;
    top: 100%;
    width: 100%;
    background-color: #fff;
  }
}

.container--restaurant--search {
  display: flex;
  align-items: center;

  &:hover {
    background-color: #f6f6f6;
  }

  .wrapper--img {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    margin-right: 25px;

    img {
      height: 100%;
      width: auto;
    }
  }
}
</style>
