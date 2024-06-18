<template>
  <div class="chat">
    <div v-for="(mensaje, index) in mensajes" :key="index" :class="mensaje.position ? 'align-start' : 'align-end'">
      <div class="user"><p>{{ mensaje.nombre }}</p></div>
      <p class="user-msg" :style="{ 'background-color': mensaje.color }">{{ mensaje.contenido }}</p>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  mensajes: Array
});
</script>

<style scoped>
.align-start {
  align-self: flex-start;
  text-align: left;
  display: flex;
  flex-direction: column;
  width: 100%;
}

.align-end {
  align-self: flex-end;
  text-align: right;
  display: flex;
  flex-direction: column;
  width: 100%;
  align-items: flex-end;
}

.chat {
  display: flex;
  flex-direction: column;
  border: 1px solid #ccc;
  padding: 10px;
  background-color: #f9f9f9;
  width: 80vh;
  height: 70vh;
  box-shadow: 0 0 5px rgba(0, 0, 0, .5);
  overflow-y: auto;
  
}

.user-msg {
  border-radius: 10px;
  padding: 0.5rem;
  word-wrap: break-word;
  max-width: 70%;
  margin: 1px;
}

.user p {
  font-weight: light;
  margin-bottom: 5px;
  color: dimgrey;
  padding: 0px;
  margin: 0px;
  
}
</style>
