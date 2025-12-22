<template>
  <header class="header">
    <div class="image">
      <img src="@/assets/images/logo.png" alt="logo_image" loading="lazy">
    </div>
    <hr>
    <ul class="projects">
      <NuxtLink v-for="i in 5" :to="$localeRoute(`/projects/${i}`)" :key="i" :class="['image' , { 'active' : i === 3 }]">
          <img src="@/assets/images/board.svg" alt="image" loading="lazy">
        <!-- <h4>Schoolna</h4> -->
      </NuxtLink>
    </ul>
  </header>
</template>

<script setup>
</script>


<style lang="scss" scoped>
  header{
    padding: 20px 0;
    background:$mainColor;
    position: fixed;
    inset-inline-start: 0;
    top: 0;
    width: 250px;
    height: 100%;
    z-index: 9;
    box-shadow: 0 0 10px #848383;
    .image{
      max-width: 180px;
      margin: 0 auto 20px;
      padding-inline: 10px;
      + hr{
        background: #e4e4e4 !important;
      }
    }
    
    ul.projects{
      margin-top: 10px;
      li{
        color: #fff;
        padding: 15px 20px;
        margin: 0 0 15px;
        max-width: 100%;
        transition: 0.3s;
        cursor: pointer;
        display: flex;
        img{
          max-width: 150px;
          filter: brightness(0) invert(0.5);
        }
        &:hover,
        &.active{
          background: #fff;
          color: $mainColor;
          img{
            filter: unset;
          }
        }
      }
    }
  }
</style>