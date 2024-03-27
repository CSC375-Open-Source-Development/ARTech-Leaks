<template>
  <div class="conversation-overview-container">
    <p class="conversation-overview-label">Conversation between</p>
    <div v-for="(user, index) in users" :key="user.id" class="conversation-overview-metadata-container">
      <img class="profile-picture" :src="require(`../../resources/profile-pictures/${user.profilePicture}`)">
      <p class="conversation-overview-label">{{ user.firstName }} {{ user.lastName }}</p>
      <p v-if="index !== users.length - 1" class="conversation-overview-label">, </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Overview',
  props: ['users'],
  computed: {
    names() {
      return this.users.map(user => `${user.firstName} ${user.lastName}`)
    },
    profilePictures() {
      return this.users.map(user => user.profilePicture)
    }
  }
}
</script>


<style scoped>
.conversation-overview-container {
  margin-bottom: 1rem;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  gap: .5rem;
  width: 100rem;
}

.conversation-overview-label {
  font-size: 1.2rem;
}

.conversation-overview-metadata-container {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}

.profile-picture {
  width: 2.5rem;
  border-radius: 5rem;
  margin-right: .2rem;
}
</style>