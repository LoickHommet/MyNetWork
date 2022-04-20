<template>
  <div class="row justify-content-center bodyAnOffice" style="box-shadow: 0em 0em 1em rgba(0, 0, 0, 0.5); wi"
  >
    <form action style="width: 100%;">
      <div>
        <h1 class="h1Office">Liste des article</h1>
        <br />
      </div>
      <div style="padding:1em">
        <div class="mb-3">
          <label for>Ajouter un article</label>
          <textarea
            type="text"
            placeholder="Texte *"
            style="width: 100%;"
            class="div4Input"
            v-model="body"
          ></textarea>
        </div>
        <button
          class="btn btn-envoyer"
          type="submit"
          v-on:click.prevent.stop="addPost()"
          style="margin: 2em 1em 2em 0em;border-radius: 12px !important;"
        >Envoyer</button>
      </div>
    </form>
  </div>
</template>
<script>
import { ref } from "@vue/reactivity";
export default {
  props: ["auth"],
  emits: ["add"],
  setup(props, context) {
    const body = ref("");
    async function addPost() {
      if (body.value) {
        const article = {
          contenu: body.value,
          urlImgArticle: "https://source.unsplash.com/random/1000x300",
          like: 0,
          pseudo: props.auth.user.pseudo,
          date: Date.now(),
          commentaires: []
        };
        const response = await fetch(`http://localhost:3001/articles`, {
          headers: {
            Accept: "application/json",
            "Content-type": "application/json"
          },
          method: "POST",
          body: JSON.stringify(article)
        }).then(resp => resp.json());
        context.emit("add", response);
        body.value = "";
      }
    }
    return { body, addPost };
  }
};
</script>



<style scoped>
.bodyAnOffice {
  background-color: #fff;
  display: block;
  margin: 0 30em 0 30em;
}

.h1Office {
  color: white;
  background-color: #283663;
  margin: 0;
  padding: 1em 2em 0em;
  font-size: 24px;
  text-align: initial;
}

.div4Input {
  padding: 1.5em !important;
  border-radius: 4px !important;
  font-size: 16px !important;
  color: #000 !important;
}

.btn-envoyer {
  background: #0094a9 !important;
  display: initial !important;
  padding: 3px 25px !important;
  color: #ffffff !important;
  border-radius: 4px !important;
  border-width: 1px !important;
  border-top-width: 1px !important;
  border-top-width: 1px !important;
  border-style: solid !important;
  border-top-style: solid !important;
  border-top-style: solid !important;
  border-color: #707070 !important;
  border-top-color: rgb(112, 112, 112) !important;
  border-top-color: rgb(112, 112, 112) !important;
  text-decoration: none !important;
}
</style>