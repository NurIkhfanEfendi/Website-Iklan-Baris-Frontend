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
                        <input name="" class="form-control" placeholder="Nama Pengguna" type="text">
                    </div>
                    <div class="form-group input-group">
                        <div class="input-group-prepend">
                            <span class="input-group-text"> <i class="fa fa-envelope"></i> </span>
                        </div>
                        <input name="" class="form-control" placeholder="Alamat Email" type="email">
                    </div>
                    <div class="form-group input-group">
                        <div class="input-group-prepend">
                            <span class="input-group-text"> <i class="fa fa-lock"></i> </span>
                        </div>
                        <input class="form-control" placeholder="Password" type="password">
                    </div>
                    <div class="form-group input-group">
                        <div class="input-group-prepend">
                            <span class="input-group-text"> <i class="fa fa-lock"></i> </span>
                        </div>
                        <input class="form-control" placeholder="Konfirmasi password" type="password">
                    </div>
                    <div class="form-group">
                        <button type="submit" class="btn btn-primary btn-block"> Create Account </button>
                    </div>
                    <p class="text-center">Have an account? <a href="/login">Log In</a> </p>
                </form>
            </article>
        </div>
    </div>
</template>
