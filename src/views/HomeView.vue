<template>
  <div>
    <el-button @click="getWeather">Get Weather</el-button>
    <el-card v-if="weatherData">{{ weatherData }}</el-card>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'
import axios from 'axios'

navigator.geolocation.getCurrentPosition(function (position) {
  geo(position.coords.latitude, position.coords.longitude)
})
let latitude: number
let longitude: number

const geo = (lat : number, lon: number) => {
  latitude = lat
  longitude = lon
}

const url = 'https://api.weather.yandex.ru/v2/informers?'

const weatherData = ref()

const getWeather = () => {
  axios.get(url, {
    headers: {
      'X-Yandex-API-Key': 'da49491d-cacf-4ecf-a756-284b4b7fa430\n'
    },
    params: {
      lat: latitude,
      lon: longitude
    }
  })
    .then(res => {
      weatherData.value = res.data
    })
    .catch(err => console.log(err))
}

</script>

<style>
.flex-grow {
  flex-grow: 1;
}
</style>
