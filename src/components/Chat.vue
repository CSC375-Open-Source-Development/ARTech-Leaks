<template>
  <div>
    <div class="container">
      <div class="conversation-box">
        <div :class="getChatUserContainerClass(message)" v-for="message in messages" :key="message.id" >
          <img class="profile-picture" :src="getProfilePicture(getUser(message))" alt="">
          <div :class="getChatContainerClass(message)">
            <div class="message-container">
              <p :class="getMessageClass(message)" v-for="element in message.body" :key="message.id + element">{{ element || '&nbsp;' }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import users from '../resources/users.json'

export default {
  name: 'Chat',
  props: ['messages'],
  methods: {
    getChatUserContainerClass(message) {
      return {
        'chat-user-container': true,
        'local-chat-user-container': !!!message.remote,
        'remote-chat-user-container': !!message.remote
      }
    },
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
    },
    getUser(message) {
      return users.find(user => user.id === message.from)
    },
    getProfilePicture(user) {
      return require(`../resources/profile-pictures/${user.profilePicture}`)
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

.chat-user-container {
  display: flex;
  align-items: center;
}

.local-chat-user-container {
  flex-direction: row-reverse;
}

.remote-chat-user-container {
  flex-direction: row;
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

.profile-picture {
  width: 2rem;
  border-radius: 5rem;
}

.message-container {
  display: flex;
  margin-right: auto;
  flex-direction: column;
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