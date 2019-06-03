<template>
  <div id="app" class="wrapper">

    <Users :users="users" @edit:user="editUser"/>
    <UsersForm :user="user" @update:user="updateUsers"/>

  </div>
</template>

<script>
//import userData
import { UserData } from './data/userData.js'
//import Components
import Users from '@/components/Users.vue'
import UsersForm from '@/components/UsersForm.vue'

export default {
  name: 'app',
  components: {
    Users,
    UsersForm
  },  
  data() {
    return {
      users: UserData,
      user: {
        type: Object
      }
    }
  },
  methods: {
    updateUsers(id, updateUser) {
       this.users = this.users.map(user =>user.id === id ? updateUser : user)
    },
    editUser(userEdit) {
      this.user = userEdit
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.wrapper {
    display:flex;
    max-width: 1000px;
    box-shadow: 0px 0px 16px -3px #dedede;
    margin: auto;
    height: 600px;
}

.wrapper >div {
    width: 50%;
}
</style>
