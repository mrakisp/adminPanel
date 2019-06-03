<template>
  <div id="user-form" class="user-form--full">
    <div class="form">
      <div>
        <label>Name</label>
         <input type="text" ref="name" :value="user.name">
         <!-- <input v-model="user.name" type="text" /> -->
      </div>
      <div>
        <label>Email</label>
        <input type="text" ref="email" :value="user.email">
      </div>
      <div>
        <label>Phone</label>
        <input type="text" ref="phone" :value="user.phone">
      </div>
      <div>
        <label>Address</label>
        <input type="text" ref="address" :value="user.address">
      </div>
      <div>
        <label>Company</label>
        <input type="text" ref="company" :value="user.company">
      </div>
      <button v-if="isEditing" @click="cancel">Cancel</button>
      <button @click="save" :disabled="!isEditing" >Save</button>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'user-form',
    props: ['user', 'test'],
    data() {
        return {
            isEditing: false,
        };
    },
    // created(){
    //   this.cachedUser = Object.assign({}, this.user);
    //   console.log(this.cachedUser)
    // },
    updated() {
      //console.log(this.user)
      //console.log(Object.keys(this.cachedUser).length)
      if(Object.keys(this.user).length !== 0){   
        this.isEditing = true;
      }
    },
    methods: {
      save() {
        //const FinalUser = Object.assign(target, source);
        this.user.name = this.$refs['name'].value;
        this.user.email = this.$refs['email'].value;
        this.user.phone = this.$refs['phone'].value;
        this.user.address = this.$refs['address'].value;
        this.user.company = this.$refs['company'].value;
        //this.cachedUser = Object.assign({}, this.user);
        this.$emit('update:user', this.user.id , this.user);
        //Object.assign(this.user, {});
        this.isEditing = false;
      },
      cancel() { 
        //Object.assign(this.user, this.cachedUser);
        this.$refs['name'].value = this.user.name ;
        this.$refs['email'].value = this.user.email;
        this.$refs['phone'].value = this.user.phone;
        this.$refs['address'].value = this.user.address;
        this.$refs['company'].value = this.user.company;
        
        //Object.assign(this.userToEdit, this.cachedUser);
      }
    }
  }
</script>