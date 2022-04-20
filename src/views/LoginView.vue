<template>
    <div class="container" style="margin-top: 2em">
       <div class="row justify-content-center bodyAnOffice" style="box-shadow: 0em 0em 1em rgba(0, 0, 0, 0.5); ">
            <form action="" style="padding: 0;">
                 <div >
					<h1 class="h1Office">Login</h1><br>
				</div>
                <div style="padding:1em">
                
                <div class="mb-3">
                    <label  class="form-label">Email :</label>
                    <input type="email" class="form-control inputOfficeP" id="inputEmail" v-model="email" required>
                </div>
                <div class="mb-3">
                    <label class="form-label">Mot de passe :</label>
                    <input type="password" class="form-control inputOfficeP" id="inputPassword" v-model="password" required>
                </div>
                <p style="color: red;">{{error}}</p>
                <button type="submit" class="btn btn-success w-100 mt-2" v-on:click.prevent.stop="login()">Se connecter</button>
                </div>
            </form>
        </div>
    </div>
</template>
<script>
import { ref } from '@vue/reactivity';
import { useRouter } from 'vue-router';
import { onMounted } from '@vue/runtime-core';

export default{
    props: ["auth", "setAuth"],
    setup(props, context) {
        const router = useRouter();
        const email = ref("");
        const password = ref("");
        const error = ref("")
        onMounted(() => {
            if (props.auth.authentified) {
                router.push('/');
            }
        })
        async function login(){
            const users = await fetch('http://localhost:3001/users').then(resp => resp.json());
            let user = users.find((us) => us.email === email.value);
            if (user && user.password === password.value) {
                error.value = "";
                props.setAuth(user, true);
                router.push("/");
            }
            else{
                error.value = "Vos identifiants ne correspondent pas.";
            }
        }
        return {email, password, error, login, router}
    },
}
</script>

<style scoped>

.bodyAnOffice{
	background-color: #FFF;
	display: block;
	
}

.h1Office{
	color: white;
	background-color: #283663;
	margin: 0;
	padding: 1em 2em 0em;
	font-size:24px;
	text-align: initial;
}
.inputOfficeP{
	
	
	padding-left: 0.5em !important;
	border-radius: 6px !important;
	
	
}
</style>
