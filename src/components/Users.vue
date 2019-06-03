<template>
  <div id="users-table" class="users">
  <div class="users__item" v-for="user in users" :key="user.id" @click="$emit('edit:user', user)">
    <div class="users__image"><img v-bind:src="user.photo"/></div>
    <div class="users__info">
      <div class="users__name" >{{ user.name }}</div>
      <div class="users__email">{{ user.email }}</div>
    </div>
  </div>
    
  </div>
</template>

<script>
export default {
  name: 'Users',
  props: {
    users: Array,
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
