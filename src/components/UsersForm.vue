<template>
  <div id="user-form">
    <div class="form">
      <div>
        <label>Name</label>
         <input type="text" ref="name" :value="user.name">
         <!-- <input v-model="user.name" type="text" /> -->
      </div>
      <div>
        <label>Email</label>
        <input type="text" ref="email" :value="user.email">
        <!-- <input v-model="user.email" type="email" /> -->
      </div>
      <div>
        <label>Phone</label>
        <input type="text" ref="phone" :value="user.phone">
        <!-- <input v-model="user.phone" type="text" /> -->
      </div>
      <div>
        <label>Address</label>
        <input type="text" ref="address" :value="user.address">
        <!-- <input v-model="user.address" type="text" /> -->
      </div>
      <div>
        <label>Company</label>
        <input type="text" ref="company" :value="user.company">
        <!-- <input v-model="user.company" type="text" /> -->
      </div>
      <button @click="save" >Save</button>
      <button @click="cancel">Cancel</button>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'user-form',
    props: {
      user: Object
    },
    mounted() {
      this.cachedUser = Object.assign({}, this.user);
    },
    methods: {
      save() {
        this.user.name = this.$refs['name'].value;
        this.user.email = this.$refs['email'].value;
        this.user.phone = this.$refs['phone'].value;
        this.user.address = this.$refs['address'].value;
        this.user.company = this.$refs['company'].value;

        this.cachedUser = Object.assign({}, this.user);
        this.$emit('update:user', this.user.id , this.user)
      },
      cancel() { 
         this.user = Object.assign({}, this.cachedUser);
      }
    }
  }
</script>

<style scoped>
.form > div {
    display: flex;
    flex-direction: column;
    text-align: left;
}
.form label {
    padding-bottom: 10px;
}
.form {
    margin-bottom: 2rem;
  }
  
</style>