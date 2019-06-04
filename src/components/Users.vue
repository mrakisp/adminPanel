<template>
  <div id="users-table" class="users" >
    <div class="users__item" v-for="user in users" 
                             :key="user.id" :class="{ 'users__item--selected' : active_el == user.id }" 
                              @click="$emit('edit:user', user), $root.$emit('send-user', user) , activate(user.id)">
      <div class="users__image">
        <img v-bind:src="user.photo"/>
      </div>
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
  },
  data() {
    return {
       active_el:0
    };
  },
  created() {
      this.$root.$on('send-saved', () => {
        this.active_el = 0
      });
    },
  methods:{
    activate(el){
        this.active_el = el;
        this.$root.$emit('send-data', el);
    }
  }
}

</script>

