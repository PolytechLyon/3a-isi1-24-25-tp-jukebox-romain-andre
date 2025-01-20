<script setup>
import PlaylistItem from "./PlaylistItem.vue";
import {onMounted, ref, watch} from "vue";
import AddMusicForm from "./AddMusicForm.vue";

let playlist = ref([]);
let currentIndex = 0;
const props = defineProps({
  next: Array,
  error: Boolean
})
const emit = defineEmits(['item']);

// extension
onMounted(() => {
  const storedPlaylist = localStorage.getItem("playlist");
  if (storedPlaylist) {
    playlist.value = JSON.parse(storedPlaylist);
  }
});

watch(() => props.next[0], () => {
  if(props.error) {
    playlist.value[currentIndex].error = true;
    // extension
    localStorage.setItem("playlist", JSON.stringify(playlist.value));
  }
  if (playlist.value.length - 1 === currentIndex) {
    if (props.next[1]) {
      currentIndex = 0;
      emit("item", {
        titre: playlist.value[currentIndex].titre,
        src: playlist.value[currentIndex].src
      });
    }
  } else {
    currentIndex = currentIndex + 1;
    emit("item", {
      titre: playlist.value[currentIndex].titre,
      src: playlist.value[currentIndex].src
    });
  }
});

function addMusic(item, type) {
  playlist.value.push({
    titre: item.titre,
    src: item.src
  });

  // extension pour conserver les URLs après rechargement de la page
  if(type==="url") {
    localStorage.setItem("playlist", JSON.stringify(playlist.value));
  }
}

function removeMusic(index) {
  playlist.value.splice(index, 1);

  // extension
  localStorage.setItem("playlist", JSON.stringify(playlist.value));
}
function playMusic(index) {
  emit("item", {
    titre: playlist.value[index].titre,
    src: playlist.value[index].src
  });
  currentIndex = index;
}
</script>

<template>
  <AddMusicForm @add="addMusic" />
  <div class="playlist-header">
    <h2>Titre</h2>
  </div>
  <ol>
    <PlaylistItem
        v-for="(item,index) in playlist"
        :titre="item.titre"
        :index="index"
        @remove="removeMusic"
        @play="playMusic"
        :error="item.error"
    />
  </ol>
</template>

<style scoped>
ol {
  display: flex;
  flex-direction: column;
  left: 0;
  right: 0;
  margin: 0;
  padding: 0;
}

.playlist-header {
  height: 40px;
  display: flex;
  flex-direction: row;
  align-items: center;
  border-bottom: 1px solid white;
  justify-content: space-between;
  padding-inline: 25px;
  padding-top: 3px;
  padding-bottom: 3px;
  color: #9a9a9a;
}
</style>