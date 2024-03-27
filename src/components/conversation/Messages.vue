<template>
  <div class="conversation-box">
    <div :class="getChatUserContainerClass(message)" v-for="message in messages" :key="message.id" >
      <img class="profile-picture" :src="getProfilePicture(message)">
      <div :class="getChatContainerClass(message)">
        <div class="message-container">
          <div class="chat-metadata-container">
            <p :class="getMetadataClass(message)">{{ getUser(message).firstName }} {{ getUser(message).lastName }}</p>
            <p :class="getMetadataClass(message)">{{ message.date }}</p>
          </div>
          <p :class="getMessageClass(message)" v-for="(element, index) in message.body" :key="message.id + index">{{ element || '&nbsp;' }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Chat',
  props: ['messages', 'users'],
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
    getMetadataClass(message) {
      return {
        metadata: true,
        'local-metadata': !!!message.remote,
        'remote-metadata': !!message.remote
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
      return this.users[message.from]
    },
    getProfilePicture(message) {
      return require(`@/resources/profile-pictures/${this.users[message.from].profilePicture}`)
    }
  }
}
</script>


<style scoped>
.conversation-box {
  display: flex;
  flex-direction: column;
  border: 1px solid #000000;
  width: 30rem;
  height: 30rem;
  padding: .4rem;
  overflow-y: scroll;
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
  max-width: 18rem;
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
  width: 2.5rem;
  border-radius: 5rem;
}

.message-container {
  display: flex;
  margin-right: auto;
  flex-direction: column;
}

.chat-metadata-container {
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: 1rem;
}

.metadata {
  margin-top: .2rem;
  margin-bottom: .4rem;
  font-size: .9rem;
  font-weight: bold;
}

.local-metadata {
  color: rgb(180, 180, 180);
}

.remote-metadata {
  color: rgb(141, 137, 137);
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