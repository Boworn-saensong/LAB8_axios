<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";

// let search = ref("");
let array = ref([]);

const options = {
  method: "GET",
  url: "https://imdb8.p.rapidapi.com/title/find",
  params: { q: "harry potter" },
  headers: {
    "X-RapidAPI-Key": "08a5fe4b84mshca6fec185cc7f9ep130a79jsnd5c198d81a11",
    "X-RapidAPI-Host": "imdb8.p.rapidapi.com",
  },
};

function loadData() {
  axios
  .request(options)
  .then(function (response) {
    array.value = response.data.results;
    console.log(response.data.results);
  })
  .catch(function (error) {
    console.error(error);
  });
}

onMounted(() => {
  loadData()
});
// const userData = ref([]);
// const url = ref("https://vuetifyjs.com/en/components/cards/#loading");

// function loadUser() {
//   axios
//     .get(url.value)
//     .then((response) => {
//       userData.value = response.data;
//     })
//     .catch((err) => {
//       console.log(err);
//     });
// }
</script>

<template>
  <div class="ma-10">
    <!-- <v-col md="4">
      <v-text-field
          v-model="search"
          model-value="harry"
          density="compact"
          variant="solo"
          label="Search templates"
          append-inner-icon="mdi-magnify"
          single-line
          hide-details
          @enter="load2"
        />
    </v-col> -->
    <v-row>
      <v-col v-for="(data, index) in array" :key="index">
        <v-card class="mx-auto" min-width="400" max-width="400" max-height="350" min-height="350">
          <v-img
            class="align-end text-white"
            height="200"
            :src="data.image.url"
            cover
          >
            <v-card-title>{{ data.title ? data.title : data.name }}</v-card-title>
          </v-img>

          <v-card-text v-if="data.knownFor">
            <h2>ผลงาน</h2>
            <div v-for="(knownFor, knownForIndex) in data.knownFor" :key="knownForIndex">
              {{ knownForIndex+1 }} {{ knownFor.title }}
            </div>
          </v-card-text>
          <v-card-text v-else>
            <h2>นักแสดงนำ</h2>
            <div v-for="(principal, principalsIndex) in data.principals" :key="principalsIndex">
              {{ principalsIndex+1 }} {{ principal.name }}
            </div>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </div>
  <!-- <h1>User view</h1>
          <h2>แสดงรายชื่อ Users......</h2>
          <button @click="loadUser()">Load User Data</button>
          <div>{{ userData }}</div>
          <ul>
              <li v-for="user in userData" :key="user.id">
                  {{ user.id }} {{ user.name }} / {{ user.address.city }} <br>
                  {{ user.address.geo.lat }} , {{ user.address.geo.lng }} 
              </li>
          </ul> -->
    <!-- <h1>{{ array }}</h1> -->
</template>

<style scoped>
</style>
