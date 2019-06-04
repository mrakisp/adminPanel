<template>
  <div id="user-form" class="user-form--full">
    <div class="form">
      <div>
        <label>Name</label>
         <input type="text" placeholder="Enter a name" v-model="initUser.name">
      </div>
      <div>
        <label>Email</label>
        <input type="email" :class="['alert', submited && isEmailValid()]" placeholder="Enter an email" v-model="initUser.email">
          <transition name="slide-fade">
            <div v-if="submited && isEmailValid()" :class="['alert', 'alert--wrong']">
                  Please enter a valid email
            </div>
          </transition>
      </div>
      <div>
        <label>Phone</label>
        <input type="text" :class="['alert', submited && isPhoneValid()]" placeholder="Enter a phone" v-model="initUser.phone">
          <transition name="slide-fade">
            <div v-if="submited && isPhoneValid()" :class="['alert', 'alert--wrong']">
                  Please enter a valid phone
            </div>
          </transition>
      </div>
      <div>
        <label>Address</label>
        <input type="text" placeholder="Enter an address" v-model="initUser.address" >
      </div>
      <div>
        <label>Company</label>
        <input type="text" placeholder="Enter a company" v-model="initUser.company" >
      </div>
      <div class="form__actions">
        <button class="form__save" @click="save" :disabled="!isEditingAlive" >Save</button>
        <button class="form__cancel" v-if="isEditingAlive" @click="cancel">Cancel</button>
      </div>  
      <transition name="slide-fade">
        <div v-if="submitedWithErrors && (isPhoneValid() || isEmailValid())" :class="['alert', 'alert--danger']">
              {{message}}
        </div>
      </transition>
      <transition name="slide-fade">
        <div v-if="submited && !submitedWithErrors && (!isPhoneValid() && !isEmailValid())" :class="['alert', 'alert--success']">
              {{message}}
        </div>
      </transition>
     
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
        regPhone: /^(\(?\+?[0-9]*\)?)?[0-9_\- \(\)]*$/,
        regEmail: /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,24}))$/,
        submited: false,
        submitedWithErrors: false,
        isEditingAlive: false,
        message: ''
      }
    },
    watch:{
      'initUser.name': function(newVal){
          if(newVal!==this.user.name){
               this.isEditingAlive = true
          }else{
            this.isEditingAlive = false
          }
      },
      'initUser.email': function(newVal){
          if(newVal!==this.user.email){
               this.isEditingAlive = true
          }else{
            this.isEditingAlive = false
          }
      },
      'initUser.phone': function(newVal){
          if(newVal!==this.user.phone){
               this.isEditingAlive = true
          }else{
            this.isEditingAlive = false
          }
      },
      'initUser.address': function(newVal){
          if(newVal!==this.user.address){
               this.isEditingAlive = true
          }else{
            this.isEditingAlive = false
          }
      },'initUser.company': function(newVal){
          if(newVal!==this.user.company){
               this.isEditingAlive = true
          }else{
            this.isEditingAlive = false
          }
      }
    },
    created() {
      this.$root.$on('send-data', (data) => {
        this.submited = false
      });
      this.$root.$on('send-user', (data) => {
        Object.assign(this.initUser, data);
      });
    },
    methods: {
      isEmailValid () {
        if (this.initUser.email && this.initUser.email.length > 0 && !this.regEmail.test(this.initUser.email) ){
          return 'has-error';
        }
      },
      isPhoneValid () {
        if (this.initUser.phone && this.initUser.phone.length > 0 && !this.regPhone.test(this.initUser.phone) ){
          return 'has-error';
        }
      },
      save() {
          this.submited = true;
          //check if email is typed correctly
          if(this.isEmailValid() === 'has-error' || this.isPhoneValid() === 'has-error'){
            this.message = 'Please correct the form errors';
            this.submitedWithErrors = true
            return
          }else{
            //Update user with saved data
            this.submitedWithErrors = false
            Object.assign(this.user, this.initUser);
            this.$emit('update:user', this.user.id , this.user);
            this.$root.$emit('send-saved');
            this.isEditingAlive = false;
            this.message = 'Succesfully Saved';
          }
      },
      cancel() { 
          //Set temp user to previous saved data
          Object.assign(this.initUser, this.user);
          this.submited= false;
          this.submitedWithErrors = false
      }
    }
  }
</script>
