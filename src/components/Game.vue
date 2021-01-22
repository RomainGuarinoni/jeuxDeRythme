<template>
  <div id="app">
    <h1>Améliore ton rythme</h1>
    <div class="gameBox">
      <div class="header">
        <div class="left">
          <p>Clique ici pour écouter l'audio :</p>
          <div class="playButton" @click="playAudio">
            <font-awesome-icon v-if="play" :icon="['fas', 'play']" />
            <p v-else style="font-size:15px">En lecture</p>
          </div>
        </div>
        <div class="right">
          <p>
            Nombre restant d'écoute :
            <span class="nbEcoute" :style="{ color: color[3 - nbEcoute] }">{{
              nbEcoute
            }}</span>
          </p>
        </div>
      </div>
      <!--<div class="metronome">
        <p>4</p>
        <p>3</p>
        <p>2</p>
        <p>1</p>
      </div>-->
      <div class="boxButton">
        <Button
          @CHECK="check"
          v-for="item in test[0].note"
          :key="item.index"
          :index="item.index"
          :indexEnCours="indexLive"
          :note="item.img"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Button from "./components/Button.vue";
export default {
  name: "App",
  components: {
    Button,
  },
  data() {
    return {
      indexLive: 0,
      nbEcoute: 3,
      play: true,
      color: ["#43A047", "#43A047", "#FBC02D", "#D50000"],
      test: [
        {
          audio: require("./assets/sound1.mp3"),
          bpm: 120,
          note: [
            {
              img: require("./assets/noir.svg"),
              index: 0,
            },
            {
              img: require("./assets/croche.svg"),
              index: 1,
            },
            {
              img: require("./assets/blanche.svg"),
              index: 2,
            },
          ],
        },
      ],
      tabNote: [],
    };
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
    check() {
      this.indexLive++;
    },
  },
  created: function shuffle() {
    var i, j, tmp;
    console.log(this.test[0].note[0]);
    for (i = this.test[0].note.length - 1; i > 0; i--) {
      j = Math.floor(Math.random() * (i + 1));
      tmp = this.test[0].note[i];
      this.test[0].note[i] = this.test[0].note[j];
      this.test[0].note[j] = tmp;
    }
  },
};
</script>

<style>
.gameBox {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  width: 100%;
  padding: 80px 0;
}
.header {
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 80%;
  padding: 80px 0;
  font-size: 20px;
}

.left {
  display: flex;
  align-items: center;
}
.nbEcoute {
  font-size: 30px;
}
.metronome {
  display: flex;
  width: 80%;
  font-size: 30px;
  justify-content: space-around;
  align-items: center;
}
.playButton {
  margin-left: 10px;
  font-size: 30px;
  cursor: pointer;
  border-radius: 10px;
  border: 2px solid black;
  width: 80px;
  height: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: all ease 200ms;
}
.playButton:hover {
  box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.411);
}

.boxButton {
  flex: 1;
  width: 80%;
  display: flex;
  justify-content: space-around;
  align-items: center;
}
</style>
