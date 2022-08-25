<script setup>
import PostTitle from "@/components/posts/PostTitle.vue";
import { reactive, ref } from "vue";
import { createUrl, pathMain } from "@/config/URIPath";

const post = reactive({
  id: "",
  name: "",
  cpf: "",
  age: "",
  city: "",
  uf: "",
  email: "",
});

const title = ref("Página de criação de pessoa");

async function postSave() {
  const data = {
    name: post.name,
    cpf: post.cpf,
    age: post.age,
    city: post.city,
    uf: post.uf,
    email: post.email,
  };
  const requestOptions = {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(data),
  };
  // console.log(requestOptions);
  await fetch(createUrl, requestOptions)
    .then((response) => {
      response.json();
      window.location.href = `${pathMain}`;
    })
    .then((json) => (post.value = json));
}
</script>

<template>
  <div>
    <PostTitle :title="title" />

    <div class="form-floating mb-3">
      <input
        type="text"
        class="form-control"
        id="name"
        placeholder="Nome"
        v-model="post.name"
      />
      <label for="title">nome</label>
    </div>
    <div class="form-floating mb-3">
      <input
        type="text"
        class="form-control"
        id="cpf"
        placeholder="CPF"
        v-model="post.cpf"
      />
      <label for="title">cpf</label>
    </div>
    <div class="form-floating mb-3">
      <input
        type="text"
        class="form-control"
        id="idade"
        placeholder="IDADE"
        v-model="post.age"
      />
      <label for="title">Idade</label>
    </div>
    <div class="form-floating mb-3">
      <input
        type="text"
        class="form-control"
        id="cidade"
        placeholder="Cidade"
        v-model="post.city"
      />
      <label for="title">Cidade</label>
    </div>
    <div class="form-floating mb-3">
      <input
        type="text"
        class="form-control"
        id="uf"
        placeholder="Estado"
        v-model="post.uf"
      />
      <label for="title">Estado</label>
    </div>
    <div class="form-floating mb-3">
      <input
        type="text"
        class="form-control"
        id="email"
        placeholder="Email"
        v-model="post.email"
      />
      <label for="title">email</label>
    </div>
    <div class="form-floating">
      <div class="container">
        <div class="row">
          <div class="d-grid gap-2 mt-4">
            <button class="btn btn-success" type="button" @click="postSave">
              Criar novo usuário
            </button>
          </div>
          <div class="d-grid gap-2 mt-4">
            <router-link to="/posts" class="btn btn-warning"
              >Cancelar</router-link
            >
          </div>
        </div>
      </div>
    </div>
    <!-- </form> -->
  </div>
</template>