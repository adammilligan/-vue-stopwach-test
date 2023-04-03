<template>
<div class="app">
  <div class="stopwatch-container">
    <div class="stopwatch time"> {{ time.hours }}:{{ time.minutes }}:{{ time.seconds }}</div>
    <div class="stopwatch buttons">
      <button
        v-if="state.state === 'paused'"
        class="play"
        style="margin-left: 50px;"
        @click="changeState"
      />
      <button
        v-if="state.state === 'playing'"
        class="paused"
        @click="changeState"
      />
      <button
        class="stop"
        style="margin-right: 50px;"
        @click="stopTimer"
      />
    </div>
  </div>
  <div class="stopwatch-add">

  </div>
</div>
</template>

<script>
export default {
  data() {
    return {
      time: {
        timer: 0,
        seconds: 0,
        minutes: 0,
        hours: 0,
      },
      state: {
        state: 'paused', // paused, playing
        stop: true,
        interval: {
          type: 'number',
        },
      },
    };
  },
  methods: {
    changeState() {
      if (this.state.state === 'paused') {
        this.startTimer();
        return;
      }

      if (this.state.paused) {
        this.startTimer();
      }

      if (this.state.play) {
        this.pauseTimer();
      }
    },
    startTimer() {
      this.state.state = 'playing';
      this.interval = setInterval(() => {
        this.time.timer += 1;
        this.time.seconds = this.time.timer % 60;
        this.time.minutes = Math.floor(this.time.timer / 60) % 60;
        this.time.hours = Math.floor(this.time.minutes / 60) % 60;
      }, 1000);
    },
    pauseTimer() {
      this.state.state = 'paused';
      clearInterval(this.interval);
    },
    stopTimer() {
      this.state.state = 'paused';
      clearInterval(this.interval);
      this.time.seconds = 0;
      this.time.minutes = 0;
      this.time.hours = 0;
    },
  },
};

</script>

<style>
.app {
  margin: 0;
  padding-top: 50px;
  box-sizing: border-box;
  display: flex;
  justify-content: space-around;
}

.stopwatch-container {
  box-sizing: border-box;
}

.stopwatch {
  width: 300px;
  height: 75px;
  display: flex;
  font-size: 40px;
  color: #9e9e9e;
  justify-content: center;
  align-items: center;
  background-color: #696969;
}

.stopwatch-add {
  width: 300px;
  height: 150px;
  background-color: #696969;
}

.time {
  flex-direction: column;
  border-bottom: 2px solid #9e9e9e;
}

.buttons {
  justify-content: space-around;
  position: relative;
}

button {
  padding: 0;
  border: none;
  font: inherit;
  color: inherit;
  background-color: transparent;
  cursor: pointer;
}

.play::after {
  content: '';
  position: absolute;
  bottom: 25px;
  left: 100px;
  border: 15px solid transparent;
  border-left: 20px solid #9e9e9e;
}

.stop {
  margin-right: 50px;
  width: 20px;
  height: 20px;
  background-color: #9e9e9e;
}

.paused::before {
  content: '';
  border-left: 5px solid #9e9e9e;
}

.paused::after {
  content: '';
  border-right: 5px solid #9e9e9e;
}
</style>
