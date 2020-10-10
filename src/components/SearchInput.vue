<template>
  <div class="searchWrapper">
    <input type="text" id="search" name="search" v-model="searchValue" @input="handleInput" />
  </div>
</template>
<script>
export default {
  name: "SearchInput"
};
</script>
<style lang="scss" scoped>
.searchWrapper {
  display: flex;
  flex-direction: column;
  width: 300px;
  margin-top: 50px;

  input {
    height: 30px;
    border: 0;
    border-bottom: 1px solid #000;
  }
}
</style>