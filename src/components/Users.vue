<template>
  <div id="users-table" class="users">
  <div class="users__item" v-for="user in users" :key="user.id" @click="$emit('edit:user', user)">
    <div class="users__image"><img v-bind:src="user.photo"/></div>
    <div class="users__info">
      <div class="users__name">{{ user.name }}</div>
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
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.users__image img {
    border-radius: 100%;
    width: 70px;
}
.users__item {
    display: flex;
    padding:6px;
}
.users__item:hover {
    background: aqua;
    cursor:pointer;
}
.users__info {
    text-align: left;
    align-self: center;
    padding-left: 25px;
}
.users {
    overflow-y: scroll;
}
</style>
