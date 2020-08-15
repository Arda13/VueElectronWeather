<template>
  <div class="container mt-2">
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <form class="form-inline m-auto my-lg-0">
        <input
          v-model="query"
          class="form-control mr-sm-2"
          type="text"
          placeholder="Search"
        />
        <button
          @click="fetchWeather"
          class="btn btn-secondary my-2 my-sm-0"
          type="button"
        >
          Search
        </button>
        {{ query }}
      </form>
    </nav>
    <div class="card border-light m-auto" style="max-width: 20rem;">
      <div class="card-header">Header</div>
      <div class="card-body">
        <h4 class="card-title">Light card title</h4>
        <p class="card-text">{{ weather.name }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import { API_URL, API_KEY } from '../lib/API';
export default {
  data() {
    return { query: '', weather: {} };
  },
  methods: {
    fetchWeather() {
      fetch(`${API_URL}weather?q=${this.query}&units=metric&APPID=${API_KEY}`)
        .then((res) => {
          return res.json();
        })
        .then(this.setResults);
    },
    setResults(results) {
      this.weather = results;
    },
  },
};
</script>

<style></style>
