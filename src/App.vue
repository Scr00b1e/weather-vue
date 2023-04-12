<template>
  <div class="app app__flex">
    <div class="app__main app__flex app__column">

      <input type="text" v-model="this.city" @keypress="getData" placeholder="City name..." class="app__input">

      <h1 v-if="cityInfo.sys">{{ cityInfo.name }}, {{ cityInfo.sys.country }}</h1>

      <div v-if="cityInfo.weather" class="app__flex app__column">
        <p>{{ cityInfo.weather[0].main }}</p>
        <p>{{ cityInfo.weather[0].description }}</p>
      </div>

      <div v-if="cityInfo.main" class="app__flex">
        <div class="app__info app__flex app__column">
          <p>{{ Math.ceil(cityInfo.main.feels_like) }}°</p>
          <p>feels lilke</p>
        </div>
        <div class="app__info app__flex app__column">
          <p>{{ Math.ceil(cityInfo.main.temp) }}</p>
          <p>temperature</p>
        </div>
        <div class="app__info app__flex app__column">
          <p>{{ cityInfo.main.pressure }}</p>
          <p>pressure</p>
        </div>
      </div>

      <div v-else class="app__flex app__column">
        <h1>Welcome!</h1>
        <p>This is weather app created by</p>
        <a href="https://github.com/Scr00b1e" target="_blank" class="app__link">@scr00b1e</a>
      </div>

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
          alert('Incorrect city name')
        } finally {
          this.city = ''
          console.log(this.cityInfo)
        }
      }
    },
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
}

*:focus {
  outline: none;
}

body {
  background-image: url('https://fixthephoto.com/blog/UserFiles/Image/222/6/10/desert-landscape-flat-design-adobe-illustrator-tutorials.png');
  background-size: cover;
  background-repeat: no-repeat;

  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}

.app {
  width: 100%;
  max-width: max-content;
  margin: 0 auto;
}

.app__flex {
  display: flex;
  align-items: center;
  justify-content: center;
}

.app__column {
  flex-direction: column;
}

.app__main {
  min-width: 500px;
  margin: 200px 0;
  padding: 20px 0;

  background: rgba(157, 154, 154, .6);
  border-radius: 20px;
}

.app__input {
  padding: 5px;
  border: 1px #000 solid;
  border-radius: 10px;
  font-size: 16px;
}

.app__info {
  margin: 10px;
  padding: 10px;

  border: 1px #000 solid;
  border-radius: 10px;
}

.app__link {
  text-decoration: none;
  color: #000;
  font-size: 18px;
  font-weight: 700;
}
</style>
