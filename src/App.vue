<template>
  <div class="top">
    <h2>Total:{{ total }}</h2>
    <h2>Time Remaining:{{ timeRemaining }}s</h2>
  </div>

  <div class="sky">
    <Duck v-if="isPlaying" :delay="1000" @hit="handleHit" />
    <Duck v-if="isPlaying" :delay="1500" @hit="handleHit" />
    <Duck v-if="isPlaying" :delay="2500" @hit="handleHit" />
    <Duck v-if="isPlaying" :delay="2000" @hit="handleHit" />
    <h1 class="score">{{score}}</h1>
  </div>

  <div class="ground">
    <div>
      <button class="btn" @click="startGame">Start</button>
    </div>
    <div>
      <button class="btn stop" @click="stopGame">Stop</button>
    </div>
  </div>

  <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Duck from "./components/Duck.vue";

export default {
  name: "App",
  components: {
    // HelloWorld
    Duck,
  },
  data() {
    return {
      score: 0,
      total: 0,
      timeRemaining: 0,
      isPlaying: false,
      delay: 1000,
    };
  },
  methods: {
    startGame() {
      const interval = setInterval(() => {
        this.timeRemaining -= 1;
        if (this.timeReinaing === 0) {
          this.stopGame();
          clearInterval(interval);
        }
      }, 1000);
      this.timeRemaining = 10;
      this.isPlaying = true;
    },
    stopGame() {
      this.isPlaying = false;
    },
    handleHit(responseTime) {
      this.score = (this.delay - responseTime) * 4;
      this.total += this.score;
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
}

.top {
  height: 10vh;
}

.sky {
  background: lightskyblue;
  height: 70vh;
  position: relative;
}

.ground {
  height: 20vh;
  background: rgb(81, 187, 81);
  display: flex;
  justify-content: space-evenly;
}
button {
  padding: 20px;
  font-size: 20px;
  width: 400px;
  background-color: rgb(25, 77, 38);
  margin-top: 15px;
}
.stop {
  background-color: rgb(148, 55, 55);
}
</style>
