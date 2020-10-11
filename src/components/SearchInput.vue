<template>
  <input
    type="text"
    id="search"
    name="search"
    :value="value"
    @input="handleChange"
    :class="{ dark: dark }"
  />
</template>
<script>
export default {
  name: "SearchInput",
  props: {
    value: {
      type: String,
      required: true
    },
    dark: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    handleChange(e) {
      this.$emit("input", e.target.value);
    }
  }
};
</script>
<style lang="scss" scoped>
input {
  margin-top: 50px;
  display: flex;
  flex-direction: column;
  width: 250px;
  height: 35px;
  color: #fff;
  text-align: center;
  font-size: 19px;
  font-weight: normal;
  border: 0;
  border-bottom: 1px solid #fff;
  outline: none;
  border-top-left-radius: 5px;
  border-top-right-radius: 5px;
  background: none;
  transition: all 0.3s ease-in-out;

  @media (min-width: 768px) {
    font-size: 21px;
    height: 45px;
  }
}

input:hover,
input:focus {
  background: rgba(139, 139, 139, 0.2);
  box-shadow: 0 10px 20px -8px rgba(255, 255, 255, 0.2);
}

.dark {
  color: #1e3d4a;
  border-bottom-color: #1e3d4a;
}

.dark:focus {
  box-shadow: 0 10px 20px -8px rgba(#1e3d4a, 0.2);
}
</style>
