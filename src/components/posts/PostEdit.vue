<script setup>
import { updateUrl, readUrl, pathMain } from "@/config/URIPath";
import PostTitle from "@/components/posts/PostTitle.vue";
import { onBeforeMount, reactive, ref } from "vue";
import { useRoute } from "vue-router";
const route = useRoute();

const post = reactive({
  id: "",
  name: "",
  cpf: "",
  age: "",
  city: "",
  uf: "",
  email: "",
});
const title = ref("é uma página para editar");

onBeforeMount(async () => {
  try {
    await fetch(readUrl + route.params.id)
      .then((response) => response.json())
      .then((json) => (post.id = json.id));
    await fetch(readUrl + route.params.id)
      .then((response) => response.json())
      .then((json) => (post.name = json.name));
    await fetch(readUrl + route.params.id)
      .then((response) => response.json())
      .then((json) => (post.cpf = json.cpf));
  } catch (error) {
    console.log(error);
  }
});

async function editSave() {
  const data = {
    name: post.name,
    cpf: post.cpf,
    age: post.age,
    city: post.city,
    uf: post.uf,
    email: post.email,
  };
  const requestOptions = {
    method: "PUT",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(data),
  };
  await fetch(updateUrl + route.params.id, requestOptions)
    .then((response) => {
      response.json();
      window.location.href = `${pathMain}posts`;
    })
    .then((json) => (post.value = json));
}
</script>

<template>
  <div>
    <PostTitle :title="title" />

    <div class="form-floating mt-3 mb-3">
      <input
        type="text"
        class="form-control"
        id="title"
        placeholder="Nome"
        v-model="post.name"
      />
      <label for="title">Nome</label>
    </div>
    <div class="form-floating mt-3 mb-3">
      <input
        type="text"
        class="form-control"
        id="title"
        placeholder="cpf"
        v-model="post.cpf"
      />
      <label for="title">CPF</label>
    </div>
    <div class="form-floating mt-3 mb-3">
      <input
        type="text"
        class="form-control"
        id="title"
        placeholder="Idade"
        v-model="post.age"
      />
      <label for="title">Idade</label>
    </div>
    <div class="form-floating mt-3 mb-3">
      <input
        type="text"
        class="form-control"
        id="title"
        placeholder="city"
        v-model="post.city"
      />
      <label for="title">Cidade</label>
    </div>
    <div class="form-floating mt-3 mb-3">
      <input
        type="text"
        class="form-control"
        id="title"
        placeholder="Estado"
        v-model="post.uf"
      />
      <label for="title">Estado</label>
    </div>
    <div class="form-floating mt-3 mb-3">
      <input
        type="text"
        class="form-control"
        id="title"
        placeholder="Email"
        v-model="post.email"
      />
      <label for="title">Email</label>
    </div>
    <div class="form-floating">
      <div class="container">
        <div class="row">
          <div class="d-grid gap-2 mt-4">
            <button class="btn btn-success" type="button" @click="editSave()">
              Salvar
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