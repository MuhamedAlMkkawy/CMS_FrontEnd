<template>
  <div class="page projects_page">
    <div class="container">
      <div class="image mazaya_logo">
        <img src="../assets/images/logo.png" alt="logo image" loading="lazy">
      </div>
      <div class="items_content items_4">
        <NuxtLink v-for="project in projectItems" :key="project.id" :to="`/modify_project/${project.id}`" :class="['content_item', { 'drafted_item': project.isDrafted }]">
          <div class="image">
            <img :src="project.image" alt="board image" loading="lazy">
          </div>
          <div class="item_control">
            <!-- <button class="edit_btn pi pi-pencil" title="edit project"></button> -->
            <button :class="['draft_btn pi', project.isDrafted ? 'pi-eye' : 'pi-eye-slash']" :title="project.isDrafted ? 'undraft project' : 'draft project'"></button>
          </div>
        </NuxtLink>
        <NuxtLink :to="$localeRoute('/modify_project')" class="content_item add_project"  title="add project">
          <i class="pi pi-plus"></i>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script setup>
  import boardImg from '@/assets/images/board.svg'

  // import { useApiAsyncData } from '@/composables/useApiFetch'


  const projectItems = ref([
    { id: 1, image: boardImg, isDrafted: false },
    // { id: 2, image: boardImg, isDrafted: true },
    // { id: 3, image: boardImg, isDrafted: false },
    // { id: 4, image: boardImg, isDrafted: true },
    // { id: 5, image: boardImg, isDrafted: false },
    // { id: 6, image: boardImg, isDrafted: true }
  ])

  // const { data } = useApiAsyncData('projects', 'https://dummyjson.com/products' , false , true);

</script>

<style lang="scss" scoped>
  .projects_page{
    background: linear-gradient(84deg, #007593 3.25%, #044D60 96.85%);
    color: #fff;
    position: relative;
    overflow: hidden;
    padding-block: 50px;
    /* Animated gradient background */
    background-size: 200% 200%;
    animation: gradientShift 8s ease infinite;
    
    /* Subtle floating particles effect */
    &::before {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: 
            radial-gradient(circle at 20% 80%, rgba(255,255,255,0.1) 2%, transparent 5%),
            radial-gradient(circle at 80% 20%, rgba(255,255,255,0.1) 2%, transparent 5%),
            radial-gradient(circle at 40% 40%, rgba(255,255,255,0.05) 3%, transparent 8%);
        animation: floatParticles 15s ease-in-out infinite;
        pointer-events: none;
    }
    .container{
      @include displayFlex($direction : column , $gap : 50px);
      min-height: 100vh;
      // background: $textColor;
      max-width: unset;
      .mazaya_logo{
        max-width: 400px;
      }
      .items_content{
        @include displayFlex($wrap : wrap , $align : stretch , $gap : 20px);
        width: 100%;
        .content_item{
          border: 1px solid #fff;
          padding: clamp(20px , 2.5vw , 50px);
          border-radius: 4px;
          transition: 0.6s;
          position: relative;
          width: 100%;
          .image{
            max-width: 180px;
            margin: 0 auto;
            filter: brightness(0)invert(1);
            transition: 1s;
          }
          .item_control{
            @include displayFlex($gap : 5px);
            position: absolute;
            top: 10px;
            inset-inline-end: 15px;
            z-index: 9;
            opacity: 0;
            button{
              border: 1px solid ;
              padding: 8px;
              font-size: 15px;
              border-radius: 4px;
              &.edit_btn{
                color: $mainColor;
                &:hover{
                  background: $mainColor;
                  color: #fff;
                }
              }
              &.draft_btn{
                color: $dangerColor;
                border-color: $dangerColor;
                &:hover{
                  background: $dangerColor;
                  color: #fff;
                }
              }
            }
          }
          &:hover{
            background: #fff;
            .image{
              filter: unset;
            }
            .item_control{
              opacity: 1;
            }
          }
        }
      }
    }
    .add_project{
      border-style:dashed !important;
      @include displayFlex();
      cursor: pointer;
      i{
        font-size: 30px;
      }
      &:hover{
        color:$mainColor;
      }
    }

  }
</style>
