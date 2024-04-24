<template>
  <button class="w-1/2 rounded-2xl text-6xl py-20 text-gray-200"
    :class="[btnStatus === true ? 'bg-[#68AE64]' : 'bg-[#C86A67]']" @click='startGame'>
    {{ btnText }}
  </button>
</template>

<script>
export default {
  name: "GoStopButton",
  props: {
    btnText: String,
    btnStatus: Boolean,
    theme: String
  },
  methods: {
    startGame() {
      this.$emit("btn-clicked", {
        btnText: this.btnText === "Go" ? "Stop" : "Go",
        btnStatus: !this.btnStatus,
      });

      if (this.btnText === "Go") {
        setTimeout(() => {
          this.$emit("btn-clicked", {
            btnText: "Stop",
            btnStatus: !this.btnStatus,
            theme: "green",
          });
        }, Math.random() * (5000 - 2000) + 2000);
      }
    }
  },
};
</script>
