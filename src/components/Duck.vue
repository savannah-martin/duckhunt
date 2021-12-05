<template>
  <div class="duck" :style="{ top: top + '%', left: left + '%' }" @click="hit">
    <img src="../assets/duck.png" alt="duck" />
  </div>
</template>

<script>
export default {
  name: "Duck",
  props: {},
  data() {
    return {
      top: 4,
      left: 40,
      isVisible: false,
      startTime: null,
    };
  },
  methods: {
    hit() {
      this.isVisible = false;
      const endTime = Date.now();
      const responseTime = this.startTime - endTime;
      this.$emit("hit", responseTime);
    },
    showDuck() {
      this.top = Math.random() * 85 + 5;
      this.left = Math.random() * 90 + 5;
      this.isVisible = true;
      this.startTime = Date.now();
    },
  },
  mounted() {
    this.showDuck();
    setInterval(() => {
      this.show.Duck();
    }, this.delay);
  },
};
</script>

<style scoped>
.duck {
  position: absolute;
  width: 80px;
  left: 70%;
  top: 50%;
  cursor: crosshair;
}

img {
  width: 100%;
}
</style>
