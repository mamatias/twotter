<template>
  <div id="app">
    @{{user.username}}
    <strong>
      {{fullName}}
    </strong>
    <small>
      {{user.email}} - Follower: {{followers}}
    </small>
    <button @click="followUser()">
      Follow
    </button>
    <div id="banner">
      <small><small><i>Msg: {{msg}}</i></small></small>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data(){
    return {
      followers:0,
      user: {
        username: 'mamatias',
        name: 'Matías',
        lastname: 'Torres',
        email: 'matiastorresrisso@gmail.com',
        isadmin: true
      },
      msg: ''
    }
  },
  watch:{
    followers(newVal, oldVal){
      if (newVal > oldVal){
        var d = new Date();
        this.msg = 'Nuevo seguidor... '+
        d.getFullYear()+'/'+
        (d.getMonth()+1)+'/'+
        d.getDate()+' '+
        d.getHours()+':'+
        d.getMinutes()+':'+
        d.getSeconds();
        console.log(d);
      }
    }
  },
  computed:{
    fullName(){
      return `${this.user.name} ${this.user.lastname}`;
    }
  },
  methods:{
    followUser(){
      this.followers = this.followers + 1;
    }
  },
  mounted(){
    this.followUser();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  /*-moz-osx-font-smoothing: grayscale;*/
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
}
#banner {
  border: 2px;
}
</style>
