<template>
  <div class="app">
    <div>
      <input type="text" v-model="this.city" @keypress="getData">

      <h1 v-if="cityInfo.sys != null">{{ cityInfo.name }}, {{ cityInfo.sys.country }}</h1>

      <div v-if="cityInfo.weather != null">
        <p>{{ cityInfo.weather[0].main }}</p>
        <p>{{ cityInfo.weather[0].description }}</p>
      </div>

      <div v-if="cityInfo.main != null">
        <p>{{ Math.ceil(cityInfo.main.feels_like) }} feels lilke</p>
        <p>{{ Math.ceil(cityInfo.main.temp) }} temp</p>
        <p>{{ cityInfo.main.pressure }} pressure</p>
      </div>

      <button @click="onData">Find</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      cityInfo: {},
      city: ''
    }
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
