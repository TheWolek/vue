<template>
  <div class="outerWrapper">
    <div class="innerWrapper">
      <div :style="style" class="photo"></div>
      <div :class="[{ Extended: DescExtended }, 'description']">
        <h2 class="title">{{ data.title }}</h2>
        <p class="descriptionP">
          {{ DescExtended ? data.fullDescription : data.description }}
          <span
            v-if="
              data.fullDescription.length > 200 &&
                !DescExtended &&
                data.fullDescription.length != data.description.length
            "
            class="learnMore"
            @click="DescExtended = !DescExtended"
            >Czytaj więcej</span
          >
          <span
            v-else-if="DescExtended"
            class="learnMore"
            @click="DescExtended = !DescExtended"
            >Czytaj mniej</span
          >
        </p>
        <p>{{ data.center }}</p>
      </div>
    </div>
    <div class="close" @click="$emit('closeModal')"></div>
  </div>
</template>
<script>
export default {
  name: "Modal",
  props: {
    image: {
      type: String,
      required: true
    },
    data: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      DescExtended: false
    };
  },
  computed: {
    style() {
      return `backgroundImage: url("${this.image}")`;
    }
  }
};
</script>
<style lang="scss" scoped>
.outerWrapper {
  background: #f9f9f9;
  width: 60%;
  height: 70%;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translateX(-50%) translateY(-50%);
  box-shadow: 0px 17px 11px -9px rgba(0, 0, 0, 0.75);
}

.close {
  position: absolute;
  width: 30px;
  height: 30px;
  padding: 30px;
  right: 0;
  top: 0;
  cursor: pointer;

  &::before,
  &::after {
    position: absolute;
    top: 30px;
    right: 20px;
    content: "";
    width: 25px;
    height: 2px;
    background: black;
    display: block;
  }

  &::before {
    transform: rotate(-45deg);
  }

  &::after {
    transform: rotate(45deg);
  }
}

.innerWrapper {
  display: flex;
  height: 100%;
  padding: 50px;
  justify-content: flex-start;
  align-items: center;
  flex-direction: row;

  .photo {
    width: 50%;
    height: 100%;
    background-size: contain;
    background-repeat: no-repeat;
    background-position: 0;
    margin-right: 20px;

    img {
      width: 100%;
    }
  }

  .description {
    width: 50%;
    height: 65%;
    color: #333;
    padding: 15px;
  }

  .title {
    color: #1e3d4a;
  }
}

.learnMore {
  color: rgb(101, 180, 255);
  text-decoration: underline;
  cursor: pointer;

  &:hover {
    color: rgb(55, 158, 255);
  }
}

.Extended {
  overflow-y: scroll;
}
</style>
