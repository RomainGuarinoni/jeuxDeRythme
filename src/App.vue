<template>
  <div id="app">
    <div class="menu" v-if="menu">
      <h1>Améliore ton rythme</h1>
      <h2>Choisis un niveau de difficulté</h2>
      <div class="levelBox">
        <div
          class="level"
          v-for="(item, index) in ['niveau 1 ', 'niveau 2 ', 'niveau 3']"
          :key="item"
          @click="goToLevel(index)"
        >
          <p>{{ item }}</p>
        </div>
      </div>
    </div>
    <div class="game" v-else>
      <Game :level="prop" />
    </div>
  </div>
</template>

<script>
import Game from "./components/Game.vue";
export default {
  name: "App",
  components: {
    Game,
  },
  data() {
    let noteGlobal = [
      {
        name: "ronde.svg",
        value: 1,
      },
      {
        name: "blanche.svg",
        value: 2,
      },
      {
        name: "noir.svg",
        value: 3,
      },
      {
        name: "noirpoint.svg",
        value: 4,
      },
      {
        name: "croche.svg",
        value: 5,
      },
      {
        name: "pause.svg",
        value: 6,
      },
      {
        name: "demiPause.svg",
        value: 7,
      },
      {
        name: "soupir.svg",
        value: 8,
      },
      {
        name: "demiSoupirPoint.svg",
        value: 9,
      },
      {
        name: "demiSoupir.svg",
        value: 10,
      },
    ];
    return {
      menu: true,
      prop: Object,
      diff: [
        [
          {
            mp3: require("@/assets/level1_1.mp3"),
            result: [2, 2],
            note: [noteGlobal[1], noteGlobal[2], noteGlobal[3], noteGlobal[4]],
          },
          {
            mp3: require("@/assets/level1_2.mp3"),
            result: [3, 3, 2],
            note: [noteGlobal[1], noteGlobal[2], noteGlobal[3], noteGlobal[4]],
          },
          {
            mp3: require("@/assets/level1_3.mp3"),
            result: [3, 3, 3, 3],
            note: [noteGlobal[1], noteGlobal[2], noteGlobal[3], noteGlobal[4]],
          },
          {
            mp3: require("@/assets/level1_4.mp3"),
            result: [2, 3, 3],
            note: [noteGlobal[1], noteGlobal[2], noteGlobal[3], noteGlobal[4]],
          },
          {
            mp3: require("@/assets/level1_5.mp3"),
            result: [3, 2, 3],
            note: [noteGlobal[1], noteGlobal[2], noteGlobal[3], noteGlobal[4]],
          },
          {
            mp3: require("@/assets/level1_6.mp3"),
            result: [3, 3, 2],
            note: [noteGlobal[1], noteGlobal[2], noteGlobal[3], noteGlobal[4]],
          },
        ],
        [],
        [],
      ],
    };
  },
  methods: {
    goToLevel(level) {
      let random = Math.floor(Math.random() * this.diff[level].length);
      this.prop = this.diff[level][random];
      console.log(this.prop);
      this.menu = false;
    },
  },
};
</script>

<style>
:root {
  --main: #424242;
}
h1,
h2 {
  color: var(--main);
  letter-spacing: 2px;
}
.menu {
  font-family: "Crete Round", serif;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 50px 0;
}
.levelBox {
  display: flex;
  flex-direction: column;
  width: 100%;
  flex: 1;
  justify-content: space-around;
  align-items: center;
}
.level {
  width: 50%;
  border: 2px solid grey;
  border-radius: 20px;
  height: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 30px;
  cursor: pointer;
  transition: all ease 200ms;
  color: var(--main);
}
.level:hover {
  box-shadow: 2px 2px 15px rgba(0, 0, 0, 0.521);
  transform: scale(1.02);
}
</style>
