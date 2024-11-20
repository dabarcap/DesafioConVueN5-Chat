<script>
export default {
  name: 'ChatBox',
  props: {
    messages: {
      type: Array,
      required: true
    },
    user1Name: {
      type: String,
      required: true
    },
    user2Name: {
      type: String,
      required: true
    }
  }
};
</script>

<template>
  <div class="chat-box">
    <!-- Iterar sobre los mensajes y mostrarlos con estilos diferentes según el propietario -->
    <div v-for="(msg, index) in messages" :key="index" class="message" :class="{'message-left': msg.name === user1Name, 'message-right': msg.name === user2Name}" :style="{ color: msg.color }">
      <p><strong>{{ msg.name }}: <br> </strong> {{ msg.message }}</p>
    </div>
  </div>
</template>

<style scoped>
.chat-box {
  width: 70%;
  padding: 10px;
  border: 1px solid #ddd;
  margin: 0 20px;
  height: 500px;
  overflow-y: auto;
}

.message {
  margin-bottom: 10px;
  display: flex;
  flex-direction: column;
}

.message p {
  margin: 0;
}

.message-left {
  align-self: flex-start; /* Alineación a la izquierda */
  background-color: #f1f0f0;
  border-radius: 10px;
  padding: 5px 10px;
  max-width: 60%;
}

.message-right {
  align-self: flex-end; /* Alineación a la derecha */
  background-color: #d0e8f5;
  border-radius: 10px;
  padding: 5px 10px;
  max-width: 60%;
}
</style>