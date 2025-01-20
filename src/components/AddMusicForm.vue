<script setup>
import {ref} from "vue";

const emit = defineEmits(['add']);
const method = ref('url');
const titre = ref('');
const url = ref('');
const file = ref(null);

function addMusic() {
  let src = '';
  if (method.value === 'url') {
    src = url.value;
    if (titre.value === "") titre.value = src;
  } else if (method.value === 'file') {
    src = URL.createObjectURL(file.value);
  }
  emit("add", {
    titre: titre.value,
    src: src
  }, method.value);
  resetForm();
}

function onFileChange(event) {
  file.value = event.target.files[0];
  titre.value = file.value.name;
}

function resetForm() {
  file.value = null;
  url.value = '';
  titre.value = '';
}
</script>

<template>
  <div class="add-form">
    <label for="method-selector">Ajouter Musique</label>
    <select v-model="method" id="method-selector" @change="resetForm">
      <option value="url">A partir d'un URL</option>
      <option value="file">A partir d'un fichier</option>
    </select>
    <input type="text" v-model="titre" placeholder="Titre">
    <div v-show="method === 'url'">
      <input v-model="url" placeholder="URL" type="text">
    </div>
    <div v-show="method === 'file'">
      <input type="file" id="file" @change="onFileChange">
      <label for="file" class="file-button">
        <svg class="file-icon" viewBox='0 0 24 24'>
          <path
              d="M18 15v3H6v-3H4v3c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2v-3h-2zM7 9l1.41 1.41L11 7.83V16h2V7.83l2.59 2.58L17 9l-5-5-5 5z"></path>
        </svg>
        Parcourir...
      </label>
    </div>
    <button class="add-button" :disabled="!file&&!url" @click="addMusic">
      <svg class="add-icon" viewBox="0 0 16 16">
        <path
            d="M15.25 8a.75.75 0 0 1-.75.75H8.75v5.75a.75.75 0 0 1-1.5 0V8.75H1.5a.75.75 0 0 1 0-1.5h5.75V1.5a.75.75 0 0 1 1.5 0v5.75h5.75a.75.75 0 0 1 .75.75z"></path>
      </svg>
    </button>
  </div>


</template>

<style scoped>

.add-form {
  background-color: #282828;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 10px;
  padding: 20px;

  border-radius: 8px;
  max-width: 800px;
  width: 100%;
  margin: 20px auto;
  box-sizing: border-box;
}

.add-form label {
  margin-right: 10px;
  color: white;
}

.add-button {
  height: 48px;
  width: 48px;
  background-color: #1db954;
  cursor: pointer;
  border: white;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  transition: background-color 0.2s ease, transform 0.2s ease;
  border-radius: 50%;
}

.add-button:hover {
  background-color: #1ed760;
  transform: scale(1.1);
}

.add-button:active {
  background-color: #1abc54;
  transform: none;
}

.add-button:disabled {
  cursor: not-allowed;
  background-color: #a18888;
  transform: none;
}

.add-icon {
  width: 32px;
  height: 32px;
  fill: black;
}

input[type=text] {
  background-color: #3e3e3e;
  border: none;
  border-radius: 4px;
  color: white;
  height: 32px;
  font-size: 14px;
  padding: 0 12px;
}

input[type=text]:focus {
  background-color: #333;
  outline: none;
  border: 1px solid #535353;
}

input[type=file] {
  display: none;
}

label.file-button {
  height: 32px;
  width: 188px;
  margin: 0;
  border-radius: 4px;
  cursor: pointer;
  background-color: white;
  color: #1db954;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  border: none;
  font-size: 16px;
  text-align: center;
  font-weight: bold;
  transition: background-color 0.2s ease, color 0.2s ease, transform 0.2s ease;
}

label.file-button:hover {
  background-color: #1db954;
  color: white;

  .file-icon {
    fill: white;
  }
;
  transform: scale(1.05);
}

label.file-button:active {
  transform: none;
}

.file-icon {
  width: 32px;
  height: 32px;
  fill: #1db954;
  transition: fill 0.2s ease
}

#method-selector {
  height: 32px;
  border-radius: 4px;
  cursor: pointer;
  background-color: #3e3e3e;
  color: white;
  border: none;
  font-size: 14px;
  text-align: center;
}
</style>