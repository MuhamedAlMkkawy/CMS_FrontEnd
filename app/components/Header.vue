<template>
  <header class="header">
    <div class="image">
      <img src="@/assets/images/logo.png" alt="logo_image" loading="lazy">
    </div>
    <hr>
    <ul class="components">
      <div
        v-for="item in sidebarComponents"
        :key="item.type"
        class="component_item"
        @click="addComponent(item.type)"
      >
        <!-- icon -->
        <i :class="item.icon" class="component_icon" />

        <!-- title -->
        <span class="component_title">
          {{ item.label }}
        </span>
      </div>
    </ul>
    <!-- <button class="control_header">
      <i class="pi pi-angle-left"></i>
    </button> -->
  </header>
</template>

<script setup>
  const sidebarComponents = [
    {
      type: 'card-slider',
      label: 'Card slider',
      icon: 'pi pi-sliders-h',
    },
    {
      type: 'nav-menu',
      label: 'Nav menu',
      icon: 'pi pi-bars',
    },
    {
      type: 'alert',
      label: 'Alert',
      icon: 'pi pi-exclamation-triangle',
    },
    {
      type: 'description-list',
      label: 'Description list',
      icon: 'pi pi-list',
    },
    {
      type: 'divider',
      label: 'Divider',
      icon: 'pi pi-minus',
    },
    {
      type: 'call-to-action',
      label: 'Call to action',
      icon: 'pi pi-phone',
    },
    {
      type: 'card',
      label: 'Card',
      icon: 'pi pi-id-card',
    },
    {
      type: 'pricing-list',
      label: 'Pricing list',
      icon: 'pi pi-tags',
    },
    {
      type: 'data-tables',
      label: 'Data tables',
      icon: 'pi pi-table',
    },
    {
      type: 'buttons',
      label: 'Buttons',
      icon: 'pi pi-clone',
    },
    {
      type: 'modal-module',
      label: 'Modal module',
      icon: 'pi pi-window-maximize',
    },
    {
      type: 'gallery',
      label: 'Gallery',
      icon: 'pi pi-images',
    },
    {
      type: 'timeline',
      label: 'Time line',
      icon: 'pi pi-clock',
    },
    {
      type: 'social-media',
      label: 'Social media',
      icon: 'pi pi-share-alt',
    },
    {
      type: 'custom-html',
      label: 'Text / custom HTML',
      icon: 'pi pi-code',
    },
    {
      type: 'heading',
      label: 'Heading',
      icon: 'pi pi-heading',
    },
    {
      type: 'accordion',
      label: 'Accordion',
      icon: 'pi pi-align-justify',
    },
    {
      type: 'contact-info',
      label: 'Contact informations',
      icon: 'pi pi-envelope',
    },
    {
      type: 'tabs',
      label: 'Tabs',
      icon: 'pi pi-folder-open',
    },
    {
      type: 'logo',
      label: 'Logo',
      icon: 'pi pi-star',
    },
    {
      type: 'back-to-top',
      label: 'Back to top',
      icon: 'pi pi-arrow-up',
    },
  ];

</script>


<style lang="scss" scoped>
  header{
    padding: 20px 0;
    background:$mainColor;
    position: fixed;
    inset-inline-start: 0;
    top: 0;
    max-width: 250px;
    width: 100%;
    height: 100vh;
    z-index: 9;
    box-shadow: 0 0 10px #8483838c;
    overflow-y: scroll;
    .image{
      max-width: 180px;
      margin: 0 auto 20px;
      padding-inline: 10px;
      // img{
      //   object-fit: contain;
      // }
      + hr{
        background: #e4e4e4 !important;
      }
    }
    
    ul.components{
      @include displayFlex($direction : column , $align : start);
      margin-top: 20px;
      .component_item{
        @include displayFlex($gap : 8px , $justify : start);
        padding: 20px 20px;
        border: 1px solid #fff;
        width: 95%;
        color: #fff;
        margin: 0 auto;
        cursor: grab;
        transition: 0.5s;
        &:hover{
          background: #fff;
          color: $mainColor;
        }
      }
    }
    // ul.projects{
    //   margin-top: 10px;
    //   a{
    //     color: #fff;
    //     padding: 15px 20px;
    //     margin: 0 0 15px;
    //     max-width: 100%;
    //     transition: 0.3s;
    //     cursor: pointer;
    //     display: flex;
    //     img{
    //       max-width: 150px;
    //       filter: brightness(0) invert(0.5);
    //     }
    //     &:hover,
    //     &.active{
    //       background: #fff;
    //       color: $mainColor;
    //       img{
    //         filter: unset;
    //       }
    //     }
    //   }
    // }
    
    // button.control_header{
    //   position: absolute;
    //   bottom: 20px;
    //   inset-inline-end: 0;
    //   background: #fff;
    //   padding: 15px;
    //   border-radius: 50%  0 0  50%;
    //   display: flex;
    //   align-items: center;
    //   transition: 0.3s;
    //   border: 1px solid;
    //   i{
    //     font-size: 25px;
    //   }
    //   &:hover{
    //     background: transparent;
    //     color: #fff;
    //   }
    // }
    &::-webkit-scrollbar{
      width: 1px ;
    }
  }
</style>