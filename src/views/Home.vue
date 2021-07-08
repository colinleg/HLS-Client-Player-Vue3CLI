<template>
  <div class="home">
    <h1>hls.js on vue 3 CLI</h1>
    <div class="container">
      <video id="player" controls></video>
    </div>
  </div>
</template>

<script>

import Hls from 'hls.js';

export default {
  name: 'Home',
  data(){
    return{
      player: null
    }
  },
  methods: {

    initHls(){
      if (Hls.isSupported()) {
        console.log('hello hls.js!');
        let player = document.querySelector('#player');
        this.player = player;
        let hls = new Hls();
        // Lier hls à la balise player
        hls.attachMedia(player);
        // L'évènement MEDIA_ATTACHED est émis par un objet HLS quand la source du média est prête
        hls.on(Hls.Events.MEDIA_ATTACHED, function () {
          console.log('player and hls.js sont liés !');
        });
        // Charger une source stream m3u8, un manifest
        // hls.loadSource('https://multiplatform-f.akamaihd.net/i/multi/april11/sintel/sintel-hd_,512x288_450_b,640x360_700_b,768x432_1000_b,1024x576_1400_m,.mp4.csmil/master.m3u8');
        // hls.loadSource('http://localhost:8000/720p.m3u8');
        hls.loadSource('ma/source/video.m3u8');
        // Quand le manifest est parsé
        hls.on(Hls.Events.MANIFEST_PARSED, function (event, data) {
          console.log(
            'manifest loaded, found ' + data.levels.length + ' quality level'
          ); // peut afficher error CORS en fonction de la source

       player.play();
        });
      }
    },
    play(){

    }
  },
  mounted(){
    this.initHls();
    this.play();
  }
}
</script>

<style scoped>
h1{
  text-align: center;
}
.container{
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>