<template>
  <div class="container">
    <ul v-for="user in data.users" :key="user.id">
      <li>ID: {{ user.id }}</li>
      <li>NAME: {{ user.nickname }}</li>
    </ul>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { Context, NuxtError } from '@nuxt/types'
import { AxiosResponse, AxiosError } from 'axios';
const axios = require('axios');
require('dotenv').config();
const url = process.env.REMO_URL;
const apiKey = process.env.REMO_KEY;

export default {
  asyncData({ params, error }: Context): Promise<object> {
    return axios.get(url, {
      headers: {
        Authorization: "Bearer " + apiKey,
        Accept: "application/json",
        "Content-Type": "application/json:charset=utf-8"
      }
    })
    .then((res: AxiosResponse) => {
      return { data: res.data[0] };
    })
    .catch((e: AxiosError) => {
      error({ statusCode: e.response !== undefined ? e.response.status : undefined, message: e.message })
    })
  }
}
// const getData = async () => {
//   const url = 'https://api.nature.global/1/devices';
//   const headers = {
//     headers: {
//       Authorization: "Bearer " + apiKey,
//       Accept: "application/json",
//       "Content-Type": "application/json:charset=utf-8"
//     }
//   };
//   const res = await fetch(url, headers);
//   const data = await res.json();
//   console.log(data[0]);
// };
// getData();

// const delayFunc = () => {
//   return new Promise((resolve, reject) => {
//     setTimeout(() => {
//       resolve('Hello World');
//     }, 3000)
//   });
// }
// delayFunc().then(value => console.log(value));
</script>

<style>

</style>
