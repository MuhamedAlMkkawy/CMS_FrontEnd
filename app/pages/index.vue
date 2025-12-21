<template>
  <div class="page projects_page">
    <div class="container">
      <div class="image mazaya_logo">
        <img src="../assets/images/logo.png" alt="logo image" loading="lazy">
      </div>
      <div class="projects_content">
        <div class="project_item">

        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
  import { useApiAsyncData } from '@/composables/useApiFetch'

  const { data } = useApiAsyncData('products', 'https://dummyjson.com/products' , false , true);
</script>

<style lang="scss" scoped>
  .projects_page{
    min-height: 100vh;
    .container{
      @include displayFlex();
    }
  }
</style>
