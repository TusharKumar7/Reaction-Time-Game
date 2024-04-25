<template>
  <div class="h-screen w-[100%] flex flex-col justify-center items-center gap-5"
    :class="[theme === 'blue' ? 'bg-[#2B87D1]' : 'bg-[#008000]']">
    <GoStopButton :btnText="btnText" @startGame="startGame" @stopGame="stopGame" />
    <ResultComponent :reactionTime="reactionTime" :highestScore="highestScore" :theme="theme"
      :isGameRunning="isGameRunning" :preciseTime="preciseTime" :second="second" />
  </div>
</template>

<script>
import GoStopButton from "./components/GoStopButton.vue";
import ResultComponent from "./components/ResultComponent.vue";

export default {
  name: "App",
  components: {
    GoStopButton,
    ResultComponent,
  },
  data() {
    return {
      btnText: "Go",
      theme: 'blue',
      isGameRunning: false,
      startTime: 0,
      reactionTime: null,
      endTime: 0,
      highestScore: 0,
      timeOut: null,
      second: 0,
    };
  },
  methods: {
    startGame() {
      if (!this.isGameRunning) {
        this.btnText = 'Stop';
        this.isGameRunning = true;
        this.timeout = setTimeout(() => {
          if (this.isGameRunning) {
            this.theme = "green";
            this.startTime = Date.now();
          }
        }, Math.floor(Math.random() * (5000 - 2000 + 1)) + 3000);
      }
    },
    stopGame() {
      if (this.isGameRunning) {
        this.btnText = 'Go';
        if (this.theme === 'green') {
          this.endTime = Date.now();
          this.calculateReactionTime();
        } else {
          this.startTime = 0;
          this.endTime = 0;
          this.reactionTime = null;
        }
        this.isGameRunning = !this.isGameRunning;
        this.theme = 'blue';
        if (this.timeout) {
          clearTimeout(this.timeout);
          this.timeout = null;
        }
      }
    },
    calculateReactionTime() {
      if (this.endTime && this.startTime) {
        this.reactionTime = this.endTime - this.startTime;
        if (this.highestScore === 0) {
          this.highestScore = this.preciseTime(this.reactionTime);
        }
        else if (this.reactionTime < this.highestScore) {
          this.highestScore = this.preciseTime(this.reactionTime);
        }
      }
    },
    preciseTime(time) {
      const seconds = Math.floor(time / 1000);
      const milliseconds = time % 1000;
      this.second = seconds;
      this.time = milliseconds.toFixed(3);
      console.log(milliseconds);
      return `${seconds}.${milliseconds.toString().padStart(3, '0')}`;
    },
  },
}
</script>
