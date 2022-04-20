<template>
    <header>
        <nav class="navbar navbar-expand-lg " style="background-color: #1f2034!important;">
            <div class="container-fluid">
                <RouterLink class="nav-brand" to="/" style="text-decoration: none;color: #FFF;">MyNetWork</RouterLink>
                
                <div class="collapse navbar-collapse" >
                    <ul class="navbar-nav" v-if="auth.authentified">
                        <li class="nav-item">
                            <RouterLink class="btn-login btn-login" to="/profil">Profil</RouterLink>
                        </li>
                    </ul>
                    <ul class="navbar-nav d-flex ms-auto" v-if="auth.authentified">
                        <li class="nav-item ms-lg-3">
                            <button class="btn btn-danger btn-login" v-on:click="setAuth(null, false)">Déconnexion</button>
                        </li>
                    </ul>
                    <ul class="navbar-nav d-flex ms-auto" v-else>
                        <li class="nav-item">
                            <RouterLink class="btn-login" to="/login">Login</RouterLink>
                        </li>
                        <li class="nav-item ms-lg-3">
                            <RouterLink class="btn-login" to="/register">Register</RouterLink>
                        </li>
                    </ul>
                </div>
            </div>
        </nav>
  </header>
</template>

<script>
import { RouterLink } from 'vue-router';

export default {
    props: ["auth", "setAuth"],
    setup(props, context){

    }
}
</script>

<style scoped>
 .btn-login{
    background: rgba(255, 255, 255, 0.17);
    border: solid 1px #dbdbdb;
    padding: 0 1em;
    font-weight: 100;
    line-height: 2.75em;
    padding: 10px 33px !important;
    text-decoration: none;
    color: rgb(255, 255, 255);
    text-transform: uppercase;
 }
</style>