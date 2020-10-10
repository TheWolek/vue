<template>
  <div class="wrapper">
    <div class="search">
      <label for="search">Test</label>
      <input type="text" id="search" name="search" v-model="searchValue" @input="handleInput" />
      <ul>
        <li v-for="item in results" :key="item.data[0].nasa_id">
          <p>{{ item.data[0].description }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import debounce from "lodash.debounce";
const API = "https://images-api.nasa.gov/search";
const KEY = "sSBVCryjStZHkLJDvE9S0z0JjDa3Jh5wax1GpUDb";

export default {
  name: "Search",
  methods: {
    handleInput: debounce(function() {
      //debugger;
      axios
        .get(`${API}?q=${this.searchValue}&media_type=image`)
        .then(res => {
          this.results = res.data.collection.items;
        })
        .catch(e => {
          console.log(e);
        });
    }, 500)
  },
  data() {
    return {
      searchValue: "",
      results: []
    };
  }
};
</script>

<style lang="scss" scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 0;
  padding: 30px;
  width: 100%;
}

.search {
  display: flex;
  flex-direction: column;
  width: 300px;

  label {
    font-family: Montserrat, sans-serif;
  }

  input {
    height: 30px;
    border: 0;
    border-bottom: 1px solid #000;
  }
}
</style>
