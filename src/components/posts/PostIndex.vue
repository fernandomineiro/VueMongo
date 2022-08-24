<script setup>
import { readUrl, createUrl, pathMain } from "@/config/URIPath";
import { onBeforeMount, ref, computed } from "vue";

const posts = ref([]);
const post = ref([]);

onBeforeMount(async () => {
  try {
    await fetch(createUrl)
      .then((response) => response.json())
      .then((json) => (posts.value = json));
  } catch (error) {
    console.log(error);
  }
});

async function postView(id) {
  try {
    await fetch(readUrl + id)
      .then((response) => response.json())
      .then((json) => (post.value = json));
  } catch (error) {
    console.log(error);
  }
}
</script>

<template>
  <table class="table table-hover table-responsive">
    <thead>
      <tr>
        <th scope="col">#</th>
        <th scope="col">Nome</th>
        <th scope="col">CPF</th>
        <th scope="col">Idade</th>
        <th scope="col">Cidade</th>
        <th scope="col">Estado</th>
        <th scope="col">Email</th>
      </tr>
    </thead>
    <tbody>
      <template v-if="posts.length > 0">
        <tr v-for="(i, index) in posts" :key="i.id">
          <th scope="row text-start">{{ index + 1 }}</th>
          <td class="text-start">
            <!-- Button trigger modal -->
            <a
              href="#"
              @click="postView(i.id)"
              data-bs-toggle="modal"
              data-bs-target="#exampleModal"
            >
              {{ i.title }}
            </a>
            <!-- Modal -->
            <div
              class="modal fade"
              id="exampleModal"
              tabindex="-1"
              aria-labelledby="exampleModalLabel"
              aria-hidden="true"
            >
              <div class="modal-dialog">
                <div class="modal-content">
                  <div class="modal-header">
                    <div class="container">
                      <div class="row">
                        <div class="col align-self-start">
                          <h5 class="modal-title" id="exampleModalLabel">
                            {{ post.name }}
                          </h5>
                        </div>
                        <div class="col align-self-center">&nbsp;</div>
                        <div class="col align-self-end">
                          <span class="text-end text-muted"
                            ><small class="extra-small">{{
                              post.id
                            }}</small></span
                          >
                        </div>
                      </div>
                    </div>

                    <button
                      type="button"
                      class="btn-close"
                      data-bs-dismiss="modal"
                      aria-label="Close"
                    ></button>
                  </div>
                  <div class="modal-body">
                    {{ post.cpf }}
                  </div>
                  <div class="modal-body">
                    {{ post.age }}
                  </div>
                  <div class="modal-body">
                    {{ post.city }}
                  </div>
                  <div class="modal-body">
                    {{ post.uf }}
                  </div>
                  <div class="modal-body">
                    {{ post.email }}
                  </div>
                  <div class="modal-footer">
                    <button
                      type="button"
                      class="btn btn-secondary"
                      data-bs-dismiss="modal"
                    >
                      Fechar
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </td>
          <td class="text-start">
            {{ i.CPF }}
          </td>
          <td class="text-end">
            <div class="btn-group">
              <router-link
                :to="{ nome: 'post-edit', params: { id: i.id } }"
                class="btn btn-outline-success btn-sm"
                >Editar</router-link
              >
              <router-link
                :to="{ nome: 'post', params: { id: i.id } }"
                class="btn btn-outline-primary btn-sm"
                >Ver</router-link
              >
              <router-link
                :to="{ nome: 'post-delete', params: { id: i.id } }"
                class="btn btn-outline-danger btn-sm"
                >Delelar</router-link
              >
            </div>
          </td>
        </tr>
      </template>
      <tr v-else>
        <td colspan="4">Sem pessoas</td>
      </tr>
    </tbody>
  </table>
</template>

<style scoped>
.extra-small {
  font-size: 0.5rem;
}
</style>