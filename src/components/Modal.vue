<template>
  <div class="outerWrapper">
    <div class="closeWrapper">
      <div class="close" @click="$emit('closeModal')"></div>
    </div>
    <div class="innerWrapper">
      <div :style="style" class="photo"></div>
      <div class="description">
        <h2 class="title">{{ data.title }}</h2>
        <p :class="[{ Extended: DescExtended }, 'descriptionP']">
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
  background: #e6e6e6;
  width: 100%;
  height: 95%;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translateX(-50%) translateY(-50%);
  box-shadow: 0px 17px 11px -9px rgba(0, 0, 0, 0.75);

  @media (min-width: 768px) {
    width: 90%;
    height: 90%;
  }

  @media (min-width: 1024px) {
    width: 60%;
    height: 70%;
  }
}

.closeWrapper {
  display: flex;
  justify-content: flex-end;
  padding: 10px 20px 0 0;
}

.close {
  //position: absolute;
  width: 30px;
  height: 30px;
  padding: 20px;
  //right: 20px;
  //top: 0;
  cursor: pointer;

  &::before,
  &::after {
    position: absolute;
    // top: 30px;
    // right: 20px;
    content: "";
    width: 25px;
    height: 2px;
    background: black;
    display: block;
  }

  @media (min-width: 768px) {
    padding: 30px;

    &::before,
    &::after {
      width: 35px;
    }
  }

  @media (min-width: 1024px) {
    padding: 20px;

    &::before,
    &::after {
      width: 25px;
    }
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
  padding: 10px 8px 8px 8px;
  height: calc(100% - 10%);
  justify-content: flex-start;
  align-items: center;
  flex-direction: column;

  @media (min-width: 768px) {
    padding: 10px 8px 8px 8px;
  }

  @media (min-width: 1024px) {
    flex-direction: row;
    padding: 50px;
  }

  .photo {
    width: 100%;
    height: 100%;
    background-size: contain;
    background-repeat: no-repeat;
    background-position: 50%;

    @media (min-width: 768px) {
    }

    @media (min-width: 1024px) {
      margin-right: 20px;
    }

    img {
      width: 100%;
    }
  }

  .descriptionP {
    height: 22vh;
    margin-top: 0;
  }

  @media (min-width: 768px) {
    .descriptionP {
      height: 12vh;
    }
  }

  @media (min-width: 1024px) {
    .descriptionP {
      height: 25vh;
      width: 20vw;
    }
  }

  .description {
    display: flex;
    flex-direction: column;
    justify-content: center;
    width: 100%;
    height: 65%;
    color: #333;
    padding: 15px 8px;

    @media (min-width: 768px) {
      flex-direction: column;
      justify-content: flex-start;
      font-size: 1.2em;
    }

    @media (min-width: 1024px) {
      width: 50%;
      height: 100%;
      padding: 15px;
    }
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
