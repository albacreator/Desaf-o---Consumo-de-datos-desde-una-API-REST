<template>
  <form @submit.prevent="handleSubmit" class="message-input">
    <select v-model="selectedUser" class="user-select">
      <option v-for="(user, index) in users" :key="index" :value="index">
        {{ user.name.first }} {{ user.name.last }}
      </option>
    </select>
    <input
      type="text"
      v-model="message"
      placeholder="Escribe tu mensaje..."
      class="input-message"
    />
    <button type="submit" class="send-button" :disabled="!message.trim()">Enviar</button>
  </form>
</template>

<script>
export default {
  name: 'MessageInputComponent',
  props: {
    users: {
      type: Array,
      required: true,
    },
    userIndex: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      message: '',
      selectedUser: this.userIndex,
    };
  },
  methods: {
    handleSubmit() {
      if (this.message.trim()) {
        this.$emit('sendMessage', this.message, this.selectedUser);
        this.message = '';
      }
    },
  },
};
</script>

<style scoped>
.message-input {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-top: 10px;
  width: 150px;
}

.user-select,
.input-message,
.send-button {
  width: 100%;
}

.user-select {
  padding: 5px;
  border-radius: 5px;
}

.input-message {
  padding: 5px;
  border: 1px solid #ddd;
  border-radius: 5px;
  width: 200px;
}

.send-button {
  padding: 5px 10px;
  background-color: #5f5f5d;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.send-button:hover {
  background-color: #5f5f5d;
}
</style>
