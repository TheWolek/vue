<template>
  <div class="claimWrapper">
    <h1 class="claim">SPACER</h1>
    <p class="subclaim">
      Begin your journey through our amazing galaxy,
      <br />and discover places you never even heard of
    </p>
    <p class="subclaim">Type anything space-related to start</p>
  </div>
</template>
<script>
export default {
  name: "Claim"
};
</script>

<style lang="scss" scoped>
.claimWrapper {
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: #e4e4e4;
}

.claim {
  font-size: 50px;

  @media (min-width: 768px) {
    font-size: 80px;
    margin-bottom: 10px;
  }
}

.subclaim {
  font-size: 15px;
  margin: 20px 0 0 0;

  @media (min-width: 768px) {
    // margin: 10px 0 0 0;
    font-size: 18px;
    letter-spacing: 1px;
  }
}
</style>