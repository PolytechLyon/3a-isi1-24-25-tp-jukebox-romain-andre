<script setup>
const props = defineProps({
  titre: String,
  index: Number,
  error: Boolean
})

const emit = defineEmits(['remove', 'play']);

function removeMusic() {
  emit('remove', props.index);
}

function playMusic() {
  emit('play', props.index);
}

</script>

<template>
  <li class="playlist-item" :class="{'error': props.error}">
    <div class="titre">{{ props.titre }}</div>
    <div>
      <button class="button" @click="playMusic">
        <svg class="icon" viewBox="0 0 16 16">
          <path
              d="M3 1.713a.7.7 0 0 1 1.05-.607l10.89 6.288a.7.7 0 0 1 0 1.212L4.05 14.894A.7.7 0 0 1 3 14.288V1.713z"></path>
        </svg>
      </button>
      <button class="button" @click="removeMusic">
        <svg class="icon" viewBox="0 0 16 16">
          <path
              d="M5.25 3v-.917C5.25.933 6.183 0 7.333 0h1.334c1.15 0 2.083.933 2.083 2.083V3h4.75v1.5h-.972l-1.257 9.544A2.25 2.25 0 0 1 11.041 16H4.96a2.25 2.25 0 0 1-2.23-1.956L1.472 4.5H.5V3h4.75zm1.5-.917V3h2.5v-.917a.583.583 0 0 0-.583-.583H7.333a.583.583 0 0 0-.583.583zM2.986 4.5l1.23 9.348a.75.75 0 0 0 .744.652h6.08a.75.75 0 0 0 .744-.652L13.015 4.5H2.985z"></path>
        </svg>
      </button>
    </div>
  </li>
</template>

<style scoped>
li {
  border-radius: 6px;
  height: 40px;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  padding-inline: 30px;
  padding-top: 3px;
  padding-bottom: 3px;
}

li:hover {
  background-color: #393939;
}

li.error {
  background-color: #d32f2f;
}

li.error:hover {
  background-color: #f44336;
}

.titre {
  color: white;
  font-weight: bold;
}

.button {
  height: 32px;
  width: 32px;
  background-color: transparent;
  cursor: pointer;
  border: white;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  transition: background-color 0.2s ease, transform 0.2s ease;
}

.button:hover {
  .icon { fill: #f0f0f0;};
  transform: scale(1.1);
}

.icon {
  width: 32px;
  height: 32px;
  fill: white;
}
</style>