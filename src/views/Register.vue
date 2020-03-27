<template>
  <div class="container ">
        <br>
        <p class="text-center">Website Iklan Baris</p>
        <hr>
        <div class="card bg-light warna">
            <article class="card-body mx-auto" style="max-width: 400px;">
                <h4 class="card-title mt-3 text-center note">Create Account</h4>
                <br>
                <form>
                    <div class="form-group input-group">
                        <div class="input-group-prepend">
                            <span class="input-group-text"> <i class="fa fa-user"></i> </span>
                        </div>
                        <input name="" class="form-control" placeholder="Nama Pengguna" type="text" v-model="name">
                    </div>
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
                    <div class="form-group input-group">
                        <div class="input-group-prepend">
                            <span class="input-group-text"> <i class="fa fa-lock"></i> </span>
                        </div>
                        <input class="form-control" placeholder="Konfirmasi password" type="password" v-model="password_confirmation">
                    </div>
                    <div class="form-group">
                        <button type="submit" href="#pablo" class="btn btn-primary btn-block"> Create Account </button>
                    </div>
                    <p class="text-center">Have an account? <a href="/login">Log In</a> </p>
                </form>
            </article>
        </div>
    </div>
</template>
<script>
export default {
    data() {
      return {
        name: '',
        email: '',
        password: '',
        password_confirmation: ''
      }
    },
    methods: {
        Register: function(){
            let name = this.name
            let email = this.email 
            let password = this.password
            let password_confirmation = this.password_confirmation
            this.$store.dispatch('register', { name, email, password, password_confirmation })
            .then(() => this.$router.push('/login'))
            .catch(err => console.log(err))
        }
    }
}
</script>
