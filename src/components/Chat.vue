<template>
  <div>
    <div class="container">
      <div class="conversation-box">
        <div v-for="message in messages" :key="message.id" :class="getChatContainerClass(message)">
          <div class="message-container">
            <p :class="getMessageClass(message)" v-for="element in message.body" :key="message.id + element">{{ element || '&nbsp;' }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Chat',
  props: ['messages'],
  methods: {
    getChatContainerClass(message) {
      return {
        'chat-container': true,
        'local-chat-container': !!!message.remote,
        'remote-chat-container': !!message.remote
      }
    },
    getMessageClass(message) {
      return {
        message: true,
        'local-message': !!!message.remote,
        'remote-message': !!message.remote
      }
    }
  }
}
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
}

.conversation-box {
  display: flex;
  flex-direction: column;
  min-width: 30rem;
  border: 1px solid #000000;
  padding: .4rem;
}

.chat-container {
  margin: .4rem;
  padding: .8rem;
  border-radius: .5rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  max-width: 17rem;
}

.local-chat-container {
  margin-left: auto;
  background: green;
}

.remote-chat-container {
  margin-right: auto;
  background: lightgrey;
}

.message-container {
  display:flex;
  margin-right:auto;
  flex-direction:column;
}

.message {
  padding: 0rem;
  margin: 0rem;
}

.local-message {
  color: white;
}

.remote-message {
  color: black;
}
</style>