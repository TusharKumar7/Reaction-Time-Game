<template>
  <div class="w-1/2 bg-[#D9EDF7] rounded-2xl text-2xl pt-4 pb-10 text-black px-5" >
    <h1 v-if="validTime">Your Reaction time was : {{ time }} seconds.</h1>
    <p v-if="validMessage">{{ message }}</p>
    <p v-if="highScoreMessage">{{ highScoreMessage }}</p>
  </div>
</template>

<script>
export default {
  name: 'ResultComponent',
  data() {
    return {
      validMessage: true,
      validTime: false,
      message: "Click Go to test your reaction time!",
      score: null,
      highScoreMessage: null,
      time:null,
    }
  },
  props:['reactionTime','highestScore','calculateReactionTime','theme','isGameRunning','preciseTime','seconds'],
  updated() {
    if (this.isGameRunning) {
      this.message = "Pay attention. Click stop when color changes";
      this.validTime = false;
      this.score = null,
      this.highScoreMessage = null
    }
    else if (this.reactionTime && this.isGameRunning === false) {
      this.validTime = true;
      this.score = true;
      this.message = "Click Go to test your reaction time!";
      this.highScoreMessage = `Your High Score is: ${this.highestScore} seconds`;
    }
    else if (!this.reactionTime) {
      this.validTime = false;
      this.message = 'Too quick... Try again!';
    } if (this.reactionTime) {
      this.time=this.preciseTime(this.reactionTime)
    }
  }
};
</script>
