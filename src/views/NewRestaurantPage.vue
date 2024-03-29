<script setup lang="ts">
import { ref } from 'vue'
import type { Restaurant } from '@/types'
import SideMenu from '../components/SideMenu.vue'
import { useRestaurantStore } from '@/stores/RestaurantStore'
import { v4 as uuidv4 } from 'uuid'

const restaurantStore = useRestaurantStore()

const newRestaurant = ref<Restaurant>({
  id: uuidv4(),
  name: '',
  address: '',
  website: '',
  status: 'Want to Try'
})
</script>

<template>
  <main class="section">
    <div class="columns">
      <SideMenu />
      <div class="column">
        <nav class="breadcrumb mb-5">
          <ul>
            <li><router-link to="/restaurants">Restaurants</router-link></li>
            <li class="is-active"><a href="#">New Restaurant</a></li>
          </ul>
        </nav>
        <form @submit.prevent>
          <div class="field">
            <div class="field">
              <label for="name" class="label">Name</label>
              <div class="control">
                <input
                  type="text"
                  class="input is-large"
                  placeholder="Domino's Pizza"
                  required
                  v-model="newRestaurant.name"
                />
              </div>
            </div>
            <div class="field">
              <label for="address" class="label">Address</label>
              <div class="control">
                <input
                  type="text"
                  class="input"
                  placeholder="Pilestredet 57,Oslo"
                  v-model="newRestaurant.address"
                />
              </div>
            </div>
            <div class="field mb-5">
              <label for="website" class="label">Website</label>
              <div class="control">
                <input
                  type="text"
                  class="input"
                  placeholder="https://www.dominos.no"
                  v-model="newRestaurant.website"
                />
              </div>
            </div>
            <div class="field">
              <div class="buttons">
                <button
                  class="button is-success"
                  @click="restaurantStore.addRestaurant(newRestaurant)"
                >
                  Create
                </button>
                <router-link to="/restaurants" class="button is-light">Cancel</router-link>
              </div>
            </div>
          </div>
        </form>
      </div>
    </div>
  </main>
</template>

<style></style>
