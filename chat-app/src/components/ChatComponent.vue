<template>
  <div class="chat-container">
    <div class="messages">
      <div
        v-for="(msg, index) in messages"
        :key="index"
        :style="{ backgroundColor: msg.color }"
        class="message"
      >
        <strong>{{ msg.user }}:</strong> {{ msg.content }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ChatComponent',
  props: {
    messages: {
      type: Array,
      required: true,
    },
    users: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
.chat-container {
  border: 1px solid #ccc;
  padding: 10px;
  height: 400px;
  overflow-y: auto;
  background-color: #fff;
  border-radius: 10px;
}

.messages {
  max-height: 300px;
  overflow-y: scroll;
}

.message {
  margin: 5px;
  padding: 10px;
  border-radius: 5px;
}
</style>


