<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios' 
import User from './components/User.vue'
import Chat from './components/Chat.vue'


const usuarios = ref([])
const mensajes = ref([])
const userPosition = (index) => {
  return index % 2 === 0;
};

onMounted(async () => {
  const url = "https://randomuser.me/api?results=2";
  try {
    const response = await axios.get(url);
    usuarios.value = response.data.results;
  } catch (error) {
    console.error("Error al obtener usuarios:", error);
  }
});

const agregarMensaje = (mensaje) => {
  mensajes.value.push(mensaje);
}
</script>

<template>
  <div class="app">
    <div class="chatUser">
    <User v-for="(user, index) in usuarios" :key="index" :nombre="user.name.first + ' ' + user.name.last" :imagen="user.picture.large" :position="userPosition(index)" @enviar-mensaje="agregarMensaje"/>
  </div>
  <div class="chat">
      <Chat :mensajes="mensajes" />
  </div>
</div>
  
</template>

<style scoped>
.app {
  display: flex;
  justify-content: center; 
  align-items: center;
  gap: 10px;
  padding: 10px;
  height: 80vh;
}

.chatUser {
  display: flex;
  flex-direction: row;
  justify-content: space-between; 
  align-items: center;
  gap: 10px;
  padding: 10px;
  width: 40%; 
}

.chat {
  align-self: center;
}
</style>

