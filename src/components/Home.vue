<template>
  <div class="hello">
    <h1>{{msg}}</h1>
    <input type="text" name="username" v-model="username"/> <br>
    <button @click="getUserData">Search</button><br><br>

    <div v-if="user != null" class="profile">
      <img :src="user.avatar_url" width="200" height="200"/><br>
      <label>Username : {{ user.login }}</label><br>
      <label>Profile name : {{ user.name }}</label><br>
      <label>Profile bio : {{ user.bio }}</label><br><br>
    </div>
  </div>  
</template>

<script>
import GithubServices from '@/services/GithubServices'

export default {
  name: 'hello',
  data () {
    return {
      msg: 'Vue PWA with Github API',
      username: '',
      user: null
    }
  },
  methods:{
    async getUserData() {
      this.user = null;

      const result = await GithubServices.searchUser({
        username: this.username
      }).then(res => {
        this.user = res.data
      }).catch(err => {
        console.log(err)
      })
      
      if(this.user !== null){
        console.log(this.user)
      }      
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
 input {
   padding:10px;
   margin:8px 0px;
 }

 button {
   padding:10px;
   border:none;
 }
</style>
