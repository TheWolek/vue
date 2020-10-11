<template>
  <div id="app">
    <div :class="[{ flexStart: step === 1, dimm: modalOpen }, 'wrapper']">
      <transition name="fade">
        <HeroImage v-if="step === 0" />
      </transition>
      <Claim v-if="step === 0" />
      <SearchInput
        v-model="searchValue"
        @input="handleInput"
        :dark="step === 1"
      />
      <div class="loader" v-if="loading" />
      <div class="results" v-if="results && !loading && step === 1">
        <Item
          v-for="item in results"
          :item="item"
          :key="item.data[0].nasa_id"
          @click.native="handleModalOpen(item)"
        />
      </div>
    </div>
    <Modal
      v-if="modalOpen"
      @closeModal="modalOpen = false"
      :image="curImg"
      :data="desc"
    />
  </div>
</template>

<script>
import axios from "axios";
import debounce from "lodash.debounce";
import HeroImage from "@/components/HeroImage";
import Claim from "@/components/Claim";
import SearchInput from "@/components/SearchInput";
import Item from "@/components/Item";
import Modal from "@/components/Modal";
const API = "https://images-api.nasa.gov/search";
const KEY = "sSBVCryjStZHkLJDvE9S0z0JjDa3Jh5wax1GpUDb";

export default {
  name: "Search",
  components: {
    HeroImage,
    Claim,
    SearchInput,
    Item,
    Modal
  },
  methods: {
    handleModalOpen(item) {
      console.log(item);
      this.modalOpen = true;
      this.curImg = item.links[0].href;
      this.desc = {
        title: item.data[0].title,
        fullDescription: item.data[0].description,
        description: item.data[0].description.substring(0, 300),
        center: item.data[0].center,
        textToShow: 300
      };
    },

    handleInput: debounce(function() {
      this.loading = true;
      axios
        .get(`${API}?q=${this.searchValue}&media_type=image`)
        .then(res => {
          this.results = res.data.collection.items;
          this.loading = false;
          this.step = 1;
        })
        .catch(e => {
          console.log(e);
        });
    }, 500)
  },
  data() {
    return {
      modalOpen: false,
      loading: false,
      step: 0,
      searchValue: "",
      results: [],
      curImg: "",
      desc: []
    };
  }
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;600;800&display=swap");

* {
  box-sizing: border-box;
}

body {
  font-family: "Montserrat", sans-serif;
  margin: 0;
  padding: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 0;
  padding: 30px;
  width: 100%;
  height: 100vh;
  min-height: 100vh;

  &.flexStart {
    justify-content: flex-start;
  }

  &.dimm {
    filter: contrast(0.4);
    pointer-events: none;
  }
}

.results {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 20px;
  margin-top: 50px;

  @media (min-width: 768px) {
    grid-template-columns: 1fr 1fr 1fr;
  }
}

.loader {
  margin-top: 100px;
  display: inline-block;
  width: 80px;
  height: 80px;
}
.loader:after {
  content: " ";
  display: block;
  width: 64px;
  height: 64px;
  margin: 8px;
  border-radius: 50%;
  border: 6px solid #1e3d4a;
  border-color: #1e3d4a transparent #1e3d4a transparent;
  animation: lds-dual-ring 1.2s linear infinite;
}
@keyframes lds-dual-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
