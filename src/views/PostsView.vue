<script setup>
import PostIndexVue from "@/components/posts/PostIndex.vue";
import PostTitleVue from "@/components/posts/PostTitle.vue";
import PostTitle from "@/components/posts/PostTitle.vue";
import { ref } from "vue";

const title = ref("Essa é uma página de pessoas");
</script>

<template>
  <div>
    <PostTitleVue :title="title" />
    <PostIndexVue />
  </div>
</template>