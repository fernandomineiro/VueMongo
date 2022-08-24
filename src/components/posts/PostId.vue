<script setup>
import { readUrl } from '@/config/URIPath';
import PostTitle from '@/components/posts/PostTitle.vue';
import { onBeforeMount, ref, computed } from 'vue';
import { useRoute } from 'vue-router'
const route = useRoute()

const post = ref([]);
const title = ref('Essa é para listar uma pessoa');
const deneme = computed(() => {
    if(route.params.id !== post.value._id) {
        return true
    }
})

onBeforeMount(async () => {
    try {
        await fetch(readUrl + route.params.id)
            .then(response => response.json())
            .then(json => post.value = json);
    } catch (error) {
        console.log(error);
    }
});

</script>

<template>
<div>
    <PostTitle :title="title" />
        <div class="card mt-3">
            <span class="text-start badge bg-light text-wrap text-muted extra-small">id: {{ post._id }}</span>
            <div class="card-body">
                <span v-if="deneme"><h3>Pessoa não encontrada!</h3></span>
                <h5 class="card-title">
                    <table>
                        <tr>
                            <td>Nome:</td>
                            <td>{{ post.name }}</td>
                        </tr>
                    </table>                    
                </h5>
                <p class="card-text">
                    <table>
                        <tr>
                            <td>CPF:</td>
                            <td>{{ post.cpf }}</td>
                        </tr>
                    </table>
                </p>
                <p class="card-text">
                    <table>
                        <tr>
                            <td>Idade:</td>
                            <td>{{ post.age }}</td>
                        </tr>
                    </table>
                </p>
                <p class="card-text">
                    <table>
                        <tr>
                            <td>city:</td>
                            <td>{{ post.city }}</td>
                        </tr>
                    </table>
                </p>
                <p class="card-text">
                    <table>
                        <tr>
                            <td>UF:</td>
                            <td>{{ post.uf }}</td>
                        </tr>
                    </table>
                </p>
                <p class="card-text">
                    <table>
                        <tr>
                            <td>Email:</td>
                            <td>{{ post.email }}</td>
                        </tr>
                    </table>
                </p>
                <div class="btn-group">
                    <router-link to="/posts" class="btn btn-outline-warning btn-sm">Voltar</router-link>
                    <router-link :to="{name:'post-edit'}" class="btn btn-outline-success btn-sm">Editar</router-link>
                    <router-link :to="{name:'post-delete'}" class="btn btn-outline-danger btn-sm">Deletar</router-link>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.extra-small {
    font-size: 0.6rem;
    font-style: italic;
}
</style>
