<template>
  <time class="clock">
    <span class="clock__hour">{{ hours }}</span>
    <span v-if="!blink || seconds % 2 === 0">:</span>
    <span v-else>&nbsp;</span>
    <span class="clock__minutes">{{ minutes }}</span>
    <span v-if="displaySeconds && (!blink || seconds % 2 === 0)">:</span>
    <span v-else-if="displaySeconds">&nbsp;</span>
    <span v-if="displaySeconds" class="clock__seconds">{{ seconds }}</span>
  </time>
</template>

<script>
function padZero(number) {
  if (number < 10) {
    return '0' + number;
  }
  return number;
}

function getDate() {
  return new Date();
}

function getDay() {
  return getDate().getDay();
}

function getMonth() {
  return getDate().getMonth();
}

function getFullYear() {
  return getDate().getFullYear();
}

function getSeconds() {
  return padZero(getDate().getSeconds());
}

function getMinutes() {
  return padZero(getDate().getMinutes());
}

function getHour() {
  return padZero(getDate().getHours());
}

export default {
  name: 'clock',
  props: {
    blink: Boolean, 
    displaySeconds: Boolean
    },

  data() {
    return {
      interval: null,
      minutes: getMinutes(),
      hours: getHour(),
      seconds: getSeconds(),
    };
  },
  methods:{
    ticker() {
      this.minutes = getMinutes();
      this.hours = getHour();
      this.seconds = getSeconds();
    }
  },

  created () {
    let _this = this;

    _this.interval = setInterval(this.ticker, 1000);
  },

  destroyed () {
    clearInterval(this.ticker);
  },

};
</script>
<style>
.clock {
    background-color: #263238;
    color: #eceff1;
    padding: .3rem .6rem;
    font-size: 3rem;
    font-family: 'Menlo', monospace;
    display: block;
  }
</style>
