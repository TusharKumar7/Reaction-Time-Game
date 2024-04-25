<template>
  <button class="w-1/2 rounded-2xl text-6xl py-20 text-gray-200"
    :class="[btnText === 'Go' ? 'bg-[#68AE64]' : 'bg-[#C86A67]']" @click="handleClick">
    {{ btnText }}
  </button>
</template>

<script>
export default {
  name: "GoStopButton",
  props: {
    btnText: String,
    startGame: Function,
    stopGame: Function,
  },

  methods: {
    handleClick() {
      if (this.btnText === "Go") {
        this.$emit("startGame");
      } else {
        this.$emit("stopGame");
      }
    },
  },
};
</script>
