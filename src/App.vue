<template>
  <div class="wrapper">
    <div class="timer" v-for="(stopwatch, idx) in this.stopwatches" :key="idx">
      <div :class="[!stopwatch.handle ? 'primary' : 'primary white']">
        {{ formatTime(stopwatch.time) }}
      </div>
      <div class="buttons">
        <div
          :class="[stopwatch.handle ? 'pause' : 'play']"
          @click="start(idx)"
        ></div>
        <div
          @click="reset(idx)"
          :class="[!stopwatch.handle ? 'reset' : 'reset whiteReset']"
        ></div>
      </div>
    </div>

    <div @click="addStopwatch" class="addTimer">
      <div class="btn">
        <img src="./assets/addBtn.png" alt="добавить" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      stopwatches: [{ handle: false, time: 0, timer: null }],
    };
  },
  methods: {
    addStopwatch() {
      this.stopwatches.push({ handle: false, time: 0, timer: null });
    },
    start(idx) {
      const stopWatch = this.stopwatches[idx];
      stopWatch.handle = !stopWatch.handle;
      if (stopWatch.handle) {
        stopWatch.timer = setInterval(() => {
          stopWatch.time++;
        }, 1000);
      }
      if (!stopWatch.handle) {
        clearInterval(stopWatch.timer);
      }
    },

    reset(idx) {
      const stopwatch = this.stopwatches[idx];
      stopwatch.time = 0;
      stopwatch.handle = false;
      clearInterval(stopwatch.timer);
    },
    formatTime(seconds) {
      const hours = Math.floor(seconds / 3600);
      const minutes = Math.floor((seconds - hours * 3600) / 60);
      const secs = seconds % 60;
      const formattedHours = hours.toString().padStart(2, "0");
      const formattedMinutes = minutes.toString().padStart(2, "0");
      const formattedSecs = secs.toString().padStart(2, "0");
      return `${formattedHours}:${formattedMinutes}:${formattedSecs}`;
    },
  },
};
</script>

<style scoped>
.wrapper {
  background-color: #353638;
  display: flex;
  flex-wrap: wrap;
  margin: 0 auto;
  justify-content: center;
  padding: 0 30%;
}

.play {
  cursor: pointer;
  width: 0;
  height: 0;
  border: solid;
  border-color: transparent transparent transparent#9E9E9E;
  border-width: 10px 10px 10px 18px;
}

.pause {
  border-style: double;
  border-width: 0px 0 0px 15px;
  border-color: #ffffff;
  height: 20px;
}

.buttons {
  height: 60px;
  display: flex;
  padding: 20px 25%;
  justify-content: space-between;
}
.reset {
  background-color: #9e9e9e;
  width: 20px;
  height: 20px;
}

.whiteReset {
  background-color: #ffffff;
}

.primary {
  height: 60px;
  color: #9e9e9e;
  font-size: 28px;
  text-align: center;
  line-height: 60px;
  border-bottom: solid #9e9e9e 2px;
}
.timer {
  margin-top: 10px;
  background-color: #696969;
  width: 225px;
  height: 120px;
  margin: 10px 10px;
}

.timer:last-child {
  margin-right: 0;
}
.white {
  color: #ffffff;
  border-bottom: solid #fafafa 2px;
}

.addTimer {
  margin-top: 10px;
  width: 225px;
  height: 120px;
  background-color: #696969;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 10px 10px;
}

.btn {
  cursor: pointer;
}

@media (max-width: 1289px) {
  .wrapper {
    padding: 0 12%;
  }
}

@media (max-width: 1023px) {
  .wrapper {
    padding: 0 16%;
  }
}

@media (max-width: 960px) {
  .wrapper {
    padding: 0 18%;
  }
}

@media (max-width: 767px) {
  .wrapper {
    padding: 0 18%;
  }
}

@media (max-width: 540px) {
  .wrapper {
    padding: 0 10%;
  }
}
</style>
