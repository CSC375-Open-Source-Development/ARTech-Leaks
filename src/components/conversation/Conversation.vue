<template>
  <div>
    <div class="container">
      <Overview :users="usersList" />
      <Messages :messages="messages" :users="usersMap" />
    </div>
  </div>
</template>

<script>
import Overview from './Overview.vue'
import Messages from './Messages.vue'

export default {
  name: 'Conversation',
  props: ['messages', 'users'],
  components: {
    Messages,
    Overview
  },
  computed: {
    usersList() {
      return this.users.sort((a, b) => `${a.firstName} ${a.lastName}`.localeCompare(`${b.firstName} ${b.lastName}`))
    },
    usersMap() {
      return this.users.reduce((acc, curr) => {
        return { ...acc, [curr.id]: curr }
      }, {})
    }
  }
}
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>