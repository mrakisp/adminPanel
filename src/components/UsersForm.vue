<template>
  <div id="user-form" class="user-form--full">
    <div class="form">
      <div>
        <label>Name</label>
         <input type="text" placeholder="Enter a name" v-model="initUser.name" :disabled="!isEditingAlive">
      </div>
      <div>
        <label>Email</label>
        <input type="email" :class="['alert', isEmailValid()]" placeholder="Enter an email" v-model="initUser.email" :disabled="!isEditingAlive">
      </div>
      <div>
        <label>Phone</label>
        <input type="text" placeholder="Enter a phone" v-model="initUser.phone" :disabled="!isEditingAlive">
      </div>
      <div>
        <label>Address</label>
        <input type="text" placeholder="Enter an address" v-model="initUser.address" :disabled="!isEditingAlive">
      </div>
      <div>
        <label>Company</label>
        <input type="text" placeholder="Enter a company" v-model="initUser.company" :disabled="!isEditingAlive">
      </div>
      <div class="form__actions">
        <button class="form__save" @click="save" :disabled="!isEditingAlive" >Save</button>
        <button class="form__cancel" v-if="isEditingAlive" @click="cancel">Cancel</button>
      </div>  
      <div v-if="submited" :class="['alert', alertType]">
            {{message}}
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
        reg: /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,24}))$/,
        submited: false,
        isEditingAlive: false,
        message: '',
        alertType: ''
      }
    },
    created() {
      this.$root.$on('send-data', (data) => {
        this.isEditingAlive = true
        this.submited = false
      });
      this.$root.$on('send-user', (data) => {
        Object.assign(this.initUser, data);
      });
    },
    methods: {
      isEmailValid () {
        return (this.initUser.email == "") ? "" : (this.reg.test(this.initUser.email)) ? '' : 'has-error';
      },
      save() {
          this.submited = true;
          if(this.isEmailValid() === 'has-error'){
            this.alertType = 'alert--danger';
            this.message = 'Please check the fields';
            return
          }
          else{
            Object.assign(this.user, this.initUser);
            this.$emit('update:user', this.user.id , this.user);
            this.$root.$emit('send-saved');
            this.isEditingAlive = false;
            this.alertType = 'alert--success';
            this.message = 'Succesfully Saved';
          }
      },
      cancel() { 
        Object.assign(this.initUser, this.user);
        this.isEmailValid()
      }
    }
  }
</script>