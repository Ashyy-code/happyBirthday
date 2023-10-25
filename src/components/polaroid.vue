<template>
  <div class="polaroid-wrap">
    <div class="polaroid">
      <div v-if="currentScene.sceneType == 'card'" class="bg-img">
        <img loading="lazy" :src=currentScene.cardBg   class="animate__animated animate__fadeIn" />
        <img loading="lazy" txt :src=currentScene.cardTextImg  v-if="currentScene.loaded" class="animate__animated animate__slideInUp animate__slower" />
      </div>
      <div v-if="currentScene.sceneType == 'team'" class="team-img">
        <img loading="lazy" :src=currentScene.team_img class="animate__animated animate__pulse animate__slower animate__infinite" />
        <h3 v-html="currentScene.team_text"></h3>
      </div>

      <div class="desc">
        <h1 v-html="currentScene.cardDesc"></h1>
      </div>

    

      <div v-if="currentScene.scene_index < sceneCount" class="next animate__animated animate__pulse animate__infinite">
        <h1>Click or Tap this card to Continue!</h1>
      </div>

      <div v-if="currentScene.scene_index == sceneCount" class="end">
        
        
        <h1>From everyone in Strategic Systems, sysDev and Reporting 🤗 </h1>
      </div>

    </div>
  </div>
</template>

<script>


export default {
  props: ["currentScene","sceneCount"],
};
</script>

<style lang="scss" scoped>
.polaroid-wrap {
  width: 100vw;
  max-width: 700px;
  height:100vh;
  margin:0rem auto;
  flex-grow: 1;
  padding-top:2rem;
  font-family: 'Bebas Neue', sans-serif;

  @media screen and (max-width:600px) {
    padding:1rem;
  }

  user-select: none;
}
.polaroid {
  background: rgba(255, 249, 227, 0.847);
  border-radius: 1rem;
  padding: 2rem;
  height:80vh;
  cursor: pointer;
  transition:all 200ms ease;
  margin-top:2rem;
  border:solid 5px #0000003d;
  display:flex;
  flex-direction: column;
  justify-content: space-between;
  

 

  &:hover{
    transform:rotate(1deg);
  }

  @media screen and (max-width:600px) {
    max-height:600px;
    padding:1rem;
    transform:none !important;
  }

    -webkit-box-shadow: 0px 0px 28px -2px rgba(0,0,0,1);
    -moz-box-shadow: 0px 0px 28px -2px rgba(0,0,0,1);
    box-shadow: 0px 0px 28px -2px rgba(0,0,0,1);
}

.bg-img {
    position:relative;
    overflow: hidden;


  img {
    width:100%;
    max-height:50vh;
    object-fit: cover;
    border-radius: 1rem;

    border:solid 5px #00000020;

    
    &[txt]{
        position: absolute;
        bottom:6%;
        left:5%;
        width:90%;
        height:unset;
        border:0;
        border-radius: 0;

    }
  }
}

.desc{
  display:grid;
  place-items: center;
  font-size:90%;
  margin:0 1rem;
  font-family: 'Montserrat', sans-serif;


  @media screen and (max-width:600px) {
    font-size:70%;
  }

  h1{
    text-align: center;
  }
}


.next{
  display:grid;
  place-items: center;
  font-size:120%;
  color:#2f75a9;



  @media screen and (max-width:600px) {
    font-size:80%;
  }

  h1{
    text-align: center;
  }
}


.team-img{
  text-align: center;
  img{
    width:100%;
    max-width:400px;
    margin:0 auto;

    @media screen and (max-width:600px) {
      max-width:200px;
    }

  }

  h3{
    font-size:160%;
    font-weight: normal;
    padding:0;
    margin:0;
    font-family: 'Montserrat', sans-serif;
    margin-top:1rem;

    @media screen and (max-width:600px) {
    font-size:110%;
  }
    
  }
}

.end{
  color:#48a35c;
  display:flex;
  justify-content: center;
  margin-top:2rem;
  font-family: 'Montserrat', sans-serif;
  text-align: center;
  font-size: 90%;

  @media screen and (max-width:600px) {
    margin-top:0;
    font-size: 60%;
    text-align: center;
    
  }
}
</style>