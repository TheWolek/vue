<template>
  <div class="wrapper">
    <Claim />
    <SearchInput />
  </div>
</template>

<script>
import axios from "axios";
import debounce from "lodash.debounce";
import Claim from "@/components/Claim";
import SearchInput from "@/components/SearchInput";
const API = "https://images-api.nasa.gov/search";
const KEY = "sSBVCryjStZHkLJDvE9S0z0JjDa3Jh5wax1GpUDb";

export default {
  name: "Search",
  components: {
    Claim,
    SearchInput
  },
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
  justify-content: center;
  margin: 0;
  padding: 30px;
  width: 100%;
  height: 100vh;
}
</style>
