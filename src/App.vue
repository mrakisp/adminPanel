<template>
  <div id="app" class="wrapper">

    <Users :users="users" @edit:user="editUser"/>
    <UsersForm :user="user" @update:user="updateUsers"/>

  </div>
</template>

<script>
//import userData
import { UserData } from './data/userData.js'
import '@/dist/style.scss'
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

</style>