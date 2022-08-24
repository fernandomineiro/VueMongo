<script setup>
import { defineProps } from "vue";

const props = defineProps({
  title: {
    type: String,
    default: "Essa é a página para add nova pessoa",
  },
});
</script>
<template>
  <div class="mb-2">
    <h1>{{ title }}</h1>
    <div class="d-grid gap-2 mt-4">
      <router-link to="/post-create" class="btn btn-primary"
        >Add nova pessoal</router-link
      >
    </div>
  </div>
</template>