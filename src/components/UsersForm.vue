<template>
  <div id="user-form" class="user-form--full">
    <div class="form">
      <div>
        <label>Name</label>
         <input type="text" ref="name" v-model="initUser.name" :disabled="!isEditingAlive">
      </div>
      <div>
        <label>Email</label>
        <input type="text" ref="email" v-model="initUser.email" :disabled="!isEditingAlive">
      </div>
      <div>
        <label>Phone</label>
        <input type="text" ref="phone" v-model="initUser.phone" :disabled="!isEditingAlive">
      </div>
      <div>
        <label>Address</label>
        <input type="text" ref="address" v-model="initUser.address" :disabled="!isEditingAlive">
      </div>
      <div>
        <label>Company</label>
        <input type="text" ref="company" v-model="initUser.company" :disabled="!isEditingAlive">
      </div>
      <div class="form__actions">
        <button class="form__save" @click="save" :disabled="!isEditingAlive" >Save</button>
        <button class="form__cancel" v-if="isEditingAlive" @click="cancel">Cancel</button>
      </div>  
    </div>
  </div>
</template>

<script>

  export default {
    name: 'user-form',
    props: ['user', 'isEditing'],
    data() {
      return {
        initUser: {
          name: null, 
          email: null, 
          phone: null,
          address: null,
          company: null,
          id: null,
          photo: null
        },
        isEditingAlive: false,
      }
    },
    created() {
      this.$root.$on('send-data', (data) => {
        this.isEditingAlive = true
      });
      this.$root.$on('send-user', (data) => {
        Object.assign(this.initUser, data);
      });
    },
    methods: {
      save() {
        Object.assign(this.user, this.initUser);
        this.$emit('update:user', this.user.id , this.user);
        this.$root.$emit('send-saved');
        this.isEditingAlive = false;
      },
      cancel() { 
        this.$refs['name'].value = this.user.name ;
        this.$refs['email'].value = this.user.email;
        this.$refs['phone'].value = this.user.phone;
        this.$refs['address'].value = this.user.address;
        this.$refs['company'].value = this.user.company;
      }
    }
  }
</script>