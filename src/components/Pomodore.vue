<template>
  <div id="app" class="container">
    <h2>
      <span>Pomodoro</span>
      <button @click="start()">
        <i class="glyphicon glyphicon-play"></i>
      </button>
    </h2>
    <div class="well">
      <div class="pomodoro-timer">
        <span>{{minute}}</span>:<span>{{second}}</span>
      </div>
    </div>  
  </div>
  
</template>

<script>
const POMODORO_STATES = {
  WORK: 'trabaja',
  REST: 'espera'
};

const WORKING_TIME_LENGTH_IN_MINUTES = 25; 
const RESTING_TIME_LENGTH_IN_MINUTES = 5;

export default {
  name: 'Pomodore',
  data() {
    return {
      minute: WORKING_TIME_LENGTH_IN_MINUTES,
      second: 0,
      pomodoroState: POMODORO_STATES.WORK,
      timestamp: 0
    }
  },
  methods:{
    start(){
      this._tick();
      this.interval = setInterval(this._tick,1000);
    },
    _tick(){
      // si el segundo no es 0, justamente disminuye segundo
      if (this.second !== 0) {
        this.second--;
        return;
      }
      //si second es 0 y minuto no es 0
      //decrementa minuto y configura second a 59
      if (this.minute !== 0) {
        this.minute--;
        this.second = 59;
        return;
      }
      //si segundo es 0 y minuto es 0,
      // intercambia intervalos trabajando/esperando 
      this.pomodoroState = this.pomodoroState === POMODORO_STATES.WORK ? POMODORO_STATES.REST : POMODORO_STATES.WORK;
      if (this.pomodoroState === POMODORO_STATES.WORK) {
        this.minute = WORKING_TIME_LENGTH_IN_MINUTES;
      } else {
        this.minute = RESTING_TIME_LENGTH_IN_MINUTES;
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
