<script>
import { RouterLink, RouterView } from 'vue-router'
import Item from './components/Item.vue';
import axios from 'axios'

export default {
  data() {
    return {
      cityInfo: {},
      city: ''
    }
  },
  components: {
    Item
  },
  methods: {
    async getData(e) {
      if (e.key == "Enter") {
        try {
          const res = await axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=imperial&appid=895284fb2d2c50a520ea537456963d9c`)
          this.cityInfo = res.data
        } catch {
          alert('Something is wrong...')
        } finally {
          this.city = ''
          console.log(this.cityInfo)
        }
      }
    },
    onData() {
      this.getData()
    }
  },
}
</script>

<template>
  <div class="app">
    <div>
      <input type="text" v-model="this.city" @keypress="getData">
      <Item :cityInfo="this.cityInfo" />
      <button @click="onData">Click me</button>
    </div>
  </div>
</template>

<style>
*,
*::after,
*::before {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background: #bebcbc;
}

.app {
  width: 100%;
  max-width: max-content;
  margin: 0 auto;
}
</style>
