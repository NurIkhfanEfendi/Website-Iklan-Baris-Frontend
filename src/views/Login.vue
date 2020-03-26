<template>
  <div class="container">
        <br>
        <p class="text-center">Website Iklan Baris</p>
        <hr>
        <div class="card bg-light warna">
            <article class="card-body mx-auto" style="max-width: 400px;">
                <div class="note">
                    <h4 class="card-title mt-3 text-center">Selamat Datang</h4>
                    <p>Silahkan login untuk memasang iklan anda.</p>
                </div>
                <br>
                <form v-on:submit.prevent="Login">
                    <div class="form-group input-group">
                        <div class="input-group-prepend">
                            <span class="input-group-text"> <i class="fa fa-envelope"></i> </span>
                        </div>
                        <input name="" class="form-control" placeholder="Alamat Email" type="email" v-model="email">
                    </div>
                    <div class="form-group input-group">
                        <div class="input-group-prepend">
                            <span class="input-group-text"> <i class="fa fa-lock"></i> </span>
                        </div>
                        <input class="form-control" placeholder="Password" type="password" v-model="password">
                    </div>
                    <div class="form-group">
                        <button type="submit" href="#pablo" class="btn btn-primary btn-block"> Masuk </button>
                    </div>
                    <p class="text-center">Don't have an account? <a href="/register">Create Account</a> </p>
                </form>
            </article>
        </div>
    </div>
</template> 
<script>
export default {
    data() {
      return {
        email: '',
        password: ''
      }
    },
    methods: {
        Login: function(){
            let email = this.email 
            let password = this.password
            this.$store.dispatch('login', { email, password })
            .then(() => this.$router.push('/'))
            .catch(err => console.log(err))
        }
    }
}
</script>
