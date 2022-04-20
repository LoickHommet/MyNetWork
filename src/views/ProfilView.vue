<template>
  <div class="container">
    <div
      class="row justify-content-center"
      v-if="user"
      style="box-shadow: 0em 0em 1em rgba(0, 0, 0, 0.5)"
    >
      <div style="background-color: #283663;">
        <h2 style="color:#FFF">Votre profil :</h2>
      </div>
      <div class="d-flex align-items-center">
        <img :src="user.urlImgProfil" alt="pp" />
      </div>
      <div class="d-flex align-items-center">
        <p class="mb-0">Pseudo :</p>
        <p class="mb-0">{{user.pseudo}}</p>
      </div>
      <div class="d-flex align-items-center">
        <p class="mb-0">Email :</p>
        <p class="mb-0">{{user.email}}</p>
      </div>
    </div>
  </div>
</template>
<script>
import { ref } from "@vue/reactivity";
import { useRouter } from "vue-router";
import { onMounted } from "@vue/runtime-core";
export default {
  props: ["auth"],
  setup(props, context) {
    const user = ref({});
    const router = useRouter();
    onMounted(async () => {
      if (!props.auth.authentified) {
        router.push("/");
      } else {
        user.value = await fetch(
          "http://localhost:3001/users/" + props.auth.user.id
        ).then(resp => resp.json());
      }
    });
    return { user, router };
  }
};
</script>
<style scoped>
img {
  width: 150px;
  clip-path: ellipse(50% 50%);
}
</style>
