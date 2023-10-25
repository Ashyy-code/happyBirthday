<template>
  <div v-if="!this.started" class="start">
    <div class="wrap">
      <img src="https://ashypls.com/endpoints/files/sarahBDAY/images/intr.png" />
      <h1>
        Hey Sarah! This year we decided to build you an interactive
        Birthday Card :D
      </h1>
      <button @click="startView()">ok.. sure.. let's see it!</button>
    </div>
  </div>

  <div
    v-if="this.started"
    class="scroller animate__animated animate__fadeIn"
    id="scroller"
  >

  <button @click="toggleMusic()" class="muter">
    <i v-if="!bgSound" class="las la-volume-mute"></i>
    <i v-if="bgSound" class="las la-volume-up"></i>
  </button>


    <polaroid
      v-for="scene in scenes"
      :key="scene.scene_index"
      :id="'plrd_' + scene.scene_index"
      @click="gotoNextScene(scene)"
      :currentScene="scene"
      :sceneCount="scenes.length"
    />
  </div>

  
</template>

<script>
import scenesData from "./assets/scenes.json";
import JSConfetti from "js-confetti";
import polaroid from "./components/polaroid.vue";


export default {
  components: { polaroid },
  mounted() {
    this.currentScene = this.scenes[0];
  },
  data() {
    return {
      scenes: scenesData,
      started: false,
      currentScene: null,
      audio2: new Audio("https://ashypls.com/endpoints/files/sarahBDAY/audio/happy.mp3"),
      audio_pop: new Audio("https://ashypls.com/endpoints/files/sarahBDAY/audio/pop.mp3"),
      bgSound:true,
    };
  },
  methods: {
    gotoNextScene(scene) {
      //exiter
      if (scene.scene_index == this.scenes.length) {
        return;
      }

      //final boop sounds
      if (scene.scene_index == this.scenes.length - 1){
        var audio = new Audio("https://ashypls.com/endpoints/files/sarahBDAY/audio/woot.mp3");
        audio.play();
      }

      //scroll enabled
      if (scene.scene_index == 1) {
        document.querySelector("#scroller").classList.add("scollenable");
      }

      let nextScene = scene.scene_index + 1;
      const blue = document.getElementById("plrd_" + nextScene);
      setTimeout(() => {
        this.scenes[nextScene - 1].loaded = true;
        const jsConfetti = new JSConfetti();
        jsConfetti.addConfetti();
        //new audio

        var audio = new Audio("https://ashypls.com/endpoints/files/sarahBDAY/audio/pop.mp3");
        audio.play();

      }, 300);
      blue.scrollIntoView();
    },
    toggleMusic(){
      this.audio2.muted = !this.audio2.muted;
      this.bgSound = !this.bgSound;
    },
    startView() {
      this.started = true;
      const jsConfetti = new JSConfetti();
      jsConfetti.addConfetti();
      this.scenes[0].loaded = true;
      var audio = new Audio("https://ashypls.com/endpoints/files/sarahBDAY/audio/woot.mp3");
      audio.play();
      //var audio2 = new Audio("https://ashypls.com/endpoints/files/sarahBDAY/audio/happy.mp3");
      this.audio2.play();
    },
  },
};
</script>

<style lang="scss" scoped>
.scroller {
  overflow-y: hidden;
  height: 100vh;
  width: 100vw;

  scroll-behavior: smooth;
}
.start {
  width: 100vw;
  height: 100vh;
  display: grid;
  place-items: center;
  font-family: "Montserrat", sans-serif;
  max-width: 700px;
  margin: 0 auto;

  .wrap {
    background: rgba(255, 255, 255, 0.847);
    border-radius: 1rem;
    padding: 2rem;
    transition: all 200ms ease;
    margin-top: 2rem;
    border: solid 5px #0000003d;
    display: flex;
    flex-direction: column;
    gap:2rem;
    transition:all 300ms ease;

    &:hover{
    transform:rotate(-1deg);
  }

    @media screen and (max-width:600px) {
      margin:0 1rem;
    }

    img {
      width: 100%;
      border-radius: 1rem;
      border: solid 5px #0000003d;
    }

    h1 {
      padding: 0;
      margin: 0;
      text-align: center;
      font-size: 180%;
      color: rgb(0, 0, 0);

      @media screen and (max-width: 600px) {
        font-size: 160%;
      }
    }

    button {
      background: #2d71e7;
      font-size: 120%;
      border: solid 3px #0000001f;
      border-radius: 1rem;
      padding: 1rem 3rem;
      text-transform: uppercase;
      color: white;
      cursor: pointer;
      transition: all 400ms ease;
      font-family: inherit;
      font-weight: bold;

      &:hover {
        background: #ffb310;
      }
    }
  }
}
.scollenable {
  overflow-y: auto;
}

.muter{
  position: fixed;
  top:1rem;
  left:1rem;
  border:0;
  background: #00000076;
  color:white;
  border-radius: 50%;
  aspect-ratio: 1;

  
  cursor: pointer;

  @media screen and (max-width:600px) {
    top:0.25rem;
    left:0.25rem;
  }

  i{
    font-size: 300%;
  }
}
</style>