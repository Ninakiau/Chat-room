<template>
  <div class="userCard" :class="{ 'align-start': position, 'align-end': !position }">
    <img :src="imagen" :alt="'Foto de ' + nombre" >
    <p>{{ nombre }}</p>
    <input type="color" v-model="colorUsuario">
    <textarea v-model="mensaje" cols="30" rows="3"></textarea>
    <button @click="enviarMensaje">Enviar</button>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
  nombre: String,
  imagen: String,
  position: Boolean
});
const mensaje = ref('');
const colorUsuario = ref('#000000');
const emit = defineEmits(['enviar-mensaje']);
const position = ref(props.position);


const enviarMensaje = () => {
  if (mensaje.value.trim() === '') return; // Evitar enviar mensajes vacíos

  // Crear un objeto mensaje con nombre, contenido y color
  const mensajeNuevo = {
    nombre: props.nombre,
    contenido: mensaje.value,
    color: colorUsuario.value,
    position: props.position
  };

  emit('enviar-mensaje', mensajeNuevo);

  mensaje.value = '';
};
</script>

<style scoped>
.align-start {
  align-items: flex-start;
}

.align-end {
  align-items: flex-end;
}

.userCard {
  display: flex;
  flex-direction: column;
  gap: 10px;
  padding: 10px;
  background-color: #fff;
  width: 200px;
  height: 80vh;
}

img {
  width: 100%;
  height: auto;
}

textarea {
  width: 97%;
  
  

}
input{
  width: 100%;
}

button {
  width: 100%;
}
</style>