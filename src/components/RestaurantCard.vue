<template>
  <div class="restaurant--card">
    <div :style="changeBackground" class="restaurant--image"></div>
    <div class="restaurant--informations">
      <div class="top">
        <p class="name">{{ inforestaurant.name }}</p>
        <p class="note">{{ inforestaurant.note }}</p>
      </div>
      <p class="time">{{ inforestaurant.drive_time }}</p>
    </div>
  </div>
</template>

<script>
import { computed } from 'vue';

export default {
  name: 'RestaurantCard',
  props: {
    inforestaurant: Object,
  },
  setup(props) {
    const changeBackground = computed(() => {
      return {
        backgroundImage: `url(${props.inforestaurant.image})`,
      };
    });

    return {
      changeBackground,
    };
  },
};
</script>

<style lang="scss">
/* CSS / SCSS */
.restaurant--card {
  width: 100%;
  height: 30vh;

  p {
    margin: 0px;
  }

  .restaurant--image {
    background-image: url('https://cn-geo1.uber.com/image-proc/resize/eats/format=webp/width=550/height=440/quality=70/srcb64=aHR0cHM6Ly9kMXJhbHNvZ25qbmczNy5jbG91ZGZyb250Lm5ldC8zNzg4MDJiMC1jNTI4LTQ4MjktYjBiNS0wY2M2NDBkZjYzY2QuanBlZw==');
    height: 70%;
    background-size: cover;
    background-position: center;
  }
  .restaurant--informations {
    .top {
      margin: 10px 0;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }
    .note {
      background-color: #eee;
      width: 30px;
      height: 30px;
      display: flex;
      align-items: center;
      justify-content: center;
      border-radius: 50%;
    }
    .time {
      font-size: 0.8rem;
    }
  }
}
</style>
