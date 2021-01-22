<template>
  <div id="gameBox">
    <p>
      {{ level.note[2].img }}
      <img :src="img" alt="note de musique" width="40px" height="40px" />
    </p>
  </div>
</template>

<script>
export default {
  name: "App",
  props: {
    level: Object,
  },

  data() {
    return {
      nbEcoute: 3,
      play: true,
      color: ["#43A047", "#43A047", "#FBC02D", "#D50000"],
    };
  },
  computed: {
    img() {
      return require("@/assets/" + this.level.note[0].name + "");
    },
  },
  methods: {
    playAudio() {
      if (this.nbEcoute > 0 && this.play == true) {
        this.play = false;
        let audio = new Audio(this.test[0].audio);
        audio.play();
        this.nbEcoute--;
        audio.addEventListener("ended", () => {
          this.play = true;
        });
      }
    },
  },
};
</script>

<style></style>
