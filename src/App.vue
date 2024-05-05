<template>
  <div :style="{ 'min-height': `${screenHeight}px` }" class="container">
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showCreateWallet: false,
      screenHeight: 0,
    };
  },
  mounted() {
    this.screenHeight = window.innerHeight;

    window.addEventListener("resize", this.updateScreenHeight);
  },
  methods: {
    updateScreenHeight() {
      this.screenHeight = window.innerHeight;
    },
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.updateScreenHeight);
  },
};
</script>

<style scoped>
.container {
  margin: 0 auto;
  max-width: 550px;
  border-left: 1px solid #4f5a703d;
  border-right: 1px solid rgba(79, 90, 112, 0.24);
  padding: 1rem;
}
</style>
