<script setup lang="ts">
import { ref } from 'vue'

type RestaurantStatus = 'Recommend' | 'Do Not Recommend' | 'Must Try'

interface Restaurant {
  name?: string
  address?: string
  status?: RestaurantStatus
  dishes?: Dish[]
}

const restaurantList = ref<Restaurant[]>([])
const newRestaurant = ref<Restaurant>({})

function addRestaurant() {
  restaurantList.value.push({
    name: newRestaurant.value.name,
    address: '',
    status: 'Recommend',
    dishes: []
  })
}
</script>

<template>
  <main>
    <!-- Create a form for adding restaurant to list -->
    <form @submit.prevent="addRestaurant">
      <div>
        <label for="restaurant-name">Restaurant Name</label>
        <input type="text" id="restaurant-name" v-model="newRestaurant.name" />
      </div>
      <div>
        <label for="restaurant-status">Restaurant Status</label>
        <input type="text" id="restaurant-status" v-model="newRestaurant.status" />
      </div>

      <button type="submit">Add Restaurant</button>
    </form>
    <ul>
      <li v-for="restaurant in restaurantList" :key="restaurant">
        {{ restaurant.name }}
      </li>
    </ul>
  </main>
</template>
