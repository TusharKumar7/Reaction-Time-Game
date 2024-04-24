<template>
  <div class="h-screen w-[100%] flex flex-col justify-center items-center gap-5"
    :class="[theme === 'blue' ? 'bg-[#2B87D1]' : 'bg-[#008000]']">
    <GoStopButton :btnText="btnText" :btnStatus="btnStatus" :theme="theme" @btn-clicked="handleBtnClicked" />
    <ResultComponent />
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
      btnStatus: true,
      theme: 'blue',
      startTime: null,
      endTime: null,
    };
  },
  computed: {
    reactionTime() {
      if (this.endTime && this.startTime) {
        return this.endTime - this.startTime;
      }
      return null;
    }
  },
  methods: {
    handleBtnClicked({ btnText, btnStatus }) {
      this.btnText = btnText;
      this.btnStatus = btnStatus;

      if (btnText === 'Stop') {
        this.endTime = Date.now();
      }
    },
    handleTheme({ theme }) {
      this.theme = theme;
    }
  }
}
</script>
