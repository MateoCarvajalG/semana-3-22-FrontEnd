<template>
    <div>
    <nav class="navbar navbar-light bg-light">
  <div class="container-fluid">
    <form class="d-flex">
      
      <button  @click.prevent="logOut"  class="btn btn-outline-success" type="button">Log Out</button>
    </form>
  </div>
</nav>
<div class="container">
    <p>
        {{user.name}}
    </p>
    <p>
        {{user.email}}
    </p>
</div>
</div>

</template>


<script >
export default{
    data(){
        return{
            user:{}
        }
    },
    methods : {
    getUserDetails(){
        let user = localStorage.getItem('user');
        let token = localStorage.getItem('jwt');
        if(token){
            this.user=JSON.parse(user);
        }
    },
    logOut(){
    localStorage.removeItem('jwt');
    localStorage.removeItem('user');
    this.$router.push('/');
    },
    },
    created(){
        this.getUserDetails();
    }

}
</script>