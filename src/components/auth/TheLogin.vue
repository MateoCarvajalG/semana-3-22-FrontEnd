<template>
    <div class="container">

<div class="row" style="margin-top:20px">
    <div class="col-xs-12 col-sm-8 col-md-6 col-sm-offset-2 col-md-offset-3">
		<form role="form">
				<h2>Please Sign In</h2>
				<hr class="colorgraph">
				<div class="form-group">
                    <input v-model="login.email" class="form-control input-lg" placeholder="Email Address">
				</div>
				<div class="form-group">
                    <input v-model="login.password" class="form-control input-lg" placeholder="Password">
				</div>
				<span class="button-checkbox">
					<button type="button" class="btn" data-color="info">Remember Me</button>
                    <input type="checkbox"  class="hidden">
					<a href="" class="btn btn-link pull-right">Forgot Password?</a>
				</span>
				<hr class="colorgraph">
				<div class="row">
					<div class="col-xs-6 col-sm-6 col-md-6">
                        <button 
                        @click.prevent="loginUser"
                        type="submit"
                        class="btn btn-lg btn-success btn-block">
                                Sign in
                        </button>
                           
					</div>
					<div class="col-xs-6 col-sm-6 col-md-6">
						<a href="" class="btn btn-lg btn-primary btn-block">Register</a>
					</div>
				</div>
            <pre>{{login}}</pre>
		</form>
	</div>
    
</div>
</div>

</template>


<script >
import swal from 'sweetalert'
export default{
    name:'TheLogin',
    data() {
        return{
            login:{
                email:'',
                password:''
            }
        }
    },

    methods:{
        async loginUser(){

            try {
                let response = await this.$http.post('/api/auth/signin', this.login)    
                 console.log(response.data)
                let token = response.data;
                let user = response.data.user;

                localStorage.setItem('jwt',token);
                localStorage.setItem('user', JSON.stringify(user));
                if (token){
                    swal("Éxitoo!!","Acceso permitido","success")
                    this.$router.push('/home')
                }
            } 
            catch(e){
                swal("Denegado","No se puede obtener acceso","error")
            }
        }

    }
}
</script>

<style  scoped>
.colorgraph {
  height: 5px;
  border-top: 0;
  background: #c4e17f;
  border-radius: 5px;
  background-image: -webkit-linear-gradient(left, #c4e17f, #c4e17f 12.5%, #f7fdca 12.5%, #f7fdca 25%, #fecf71 25%, #fecf71 37.5%, #f0776c 37.5%, #f0776c 50%, #db9dbe 50%, #db9dbe 62.5%, #c49cde 62.5%, #c49cde 75%, #669ae1 75%, #669ae1 87.5%, #62c2e4 87.5%, #62c2e4);
  background-image: -moz-linear-gradient(left, #c4e17f, #c4e17f 12.5%, #f7fdca 12.5%, #f7fdca 25%, #fecf71 25%, #fecf71 37.5%, #f0776c 37.5%, #f0776c 50%, #db9dbe 50%, #db9dbe 62.5%, #c49cde 62.5%, #c49cde 75%, #669ae1 75%, #669ae1 87.5%, #62c2e4 87.5%, #62c2e4);
  background-image: -o-linear-gradient(left, #c4e17f, #c4e17f 12.5%, #f7fdca 12.5%, #f7fdca 25%, #fecf71 25%, #fecf71 37.5%, #f0776c 37.5%, #f0776c 50%, #db9dbe 50%, #db9dbe 62.5%, #c49cde 62.5%, #c49cde 75%, #669ae1 75%, #669ae1 87.5%, #62c2e4 87.5%, #62c2e4);
  background-image: linear-gradient(to right, #c4e17f, #c4e17f 12.5%, #f7fdca 12.5%, #f7fdca 25%, #fecf71 25%, #fecf71 37.5%, #f0776c 37.5%, #f0776c 50%, #db9dbe 50%, #db9dbe 62.5%, #c49cde 62.5%, #c49cde 75%, #669ae1 75%, #669ae1 87.5%, #62c2e4 87.5%, #62c2e4);
}
</style>