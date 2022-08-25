<script setup>
import { deleteUrl, readUrl, pathMain } from "@/config/URIPath";
import PostTitle from "@/components/posts/PostTitle.vue";
import { onBeforeMount, ref, computed } from "vue";
import { useRoute } from "vue-router";
const route = useRoute();

const post = ref([]);

const title = ref("TEssa é página para deletar pessoa");

const btn = ref("Perigo");

const deneme = computed(() => {
  if (route.params.id !== post.value.id) {
    return true;
  }
});

onBeforeMount(async () => {
  try {
    await fetch(readUrl + route.params.id)
      .then((response) => response.json())
      .then((json) => (post.value = json));
  } catch (error) {
    console.log(error);
  }
});

async function deletePost() {
  const requestOptions = {
    method: "DELETE",
    headers: { "Content-Type": "application/json" },
  };
  await fetch(deleteUrl + route.params.id, requestOptions)
    .then((response) => {
      response.json();
      window.location.href = `${pathMain}posts`;
    })
    .catch((error) => console.log(error));
}
</script>
<template>
  <div>
    <PostTitle :title="title" />
    <div class="card mt-3">
      <span class="text-start badge bg-light text-wrap text-muted extra-small"
        >id: {{ post.id }}</span
      >
      <div class="card-body">
        <span v-if="deneme">
          <h3>Pessoa não encontrada!</h3>
        </span>
        <h5 class="card-title">{{ post.name }}</h5>
        <p class="card-text">{{ post.cpf }}</p>
        <div class="container">
          <div class="row">
            <div class="d-grid gap-2 mt-4">
              <button
                @mouseover="btn = 'success'"
                @mouseleave="btn = 'danger'"
                :class="'btn btn-block btn-' + btn"
                @click="deletePost"
              >
                {{
                  btn == "danger"
                    ? "Você deseja deletar essa pessoa?"
                    : "Sim eu quero deletar."
                }}
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
    </div>
  </div>
</template>

<style>
.extra-small {
  font-size: 0.6rem;
  font-style: italic;
}
</style>