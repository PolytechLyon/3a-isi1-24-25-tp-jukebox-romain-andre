<script setup>
import AudioController from './components/AudioController.vue'
import Playlist from "./components/Playlist.vue";
import {ref} from "vue";

const srcAudio = ref('');
const titre = ref('');
const load = ref(false);
const error = ref(false);
const next = ref([false]);

function handleEnded(currentState, err) {
  error.value = err === "error";

  if (currentState === "aucun") {
    next.value[0] = !next.value[0];
    next.value[1] = false
  } else if (currentState === "liste") {
    next.value[0] = !next.value[0];
    next.value[1] = true
  } else if (currentState === "titre") {
    load.value = !load.value;
  }
}

function changeSrc(item) {
  srcAudio.value = item.src;
  titre.value = item.titre;
  load.value = !load.value;
}
</script>

<template>
  <header>
    <img src="../public/jukebox.png" alt="icon">
    <h1>Jukebox</h1>
  </header>
  <Playlist @item="changeSrc" :next="next" :error="error"/>
  <AudioController :src-audio="srcAudio" :titre="titre" :load="load" @ended="handleEnded"/>
</template>

<style scoped>
header {
  position: relative;
  background-color: black;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 3px 25px;
}

header img {
  height: 65px;
  width: 65px;
  margin-right: auto;
}

header h1 {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  color: white;
  font-size: 55px;
  animation: colorChange 3s ease-in-out infinite alternate;
}

@keyframes colorChange {
  0% {
    color: #fff;
  }
  100% {
    color: #1DB954;
  }
}
</style>
