<template>
  <div class="project_page page">
    <div class="container project_content">
      <div class="pages">
        <button
          v-for="i in 8"
          :key="i"
          :class="['page_item', { active: activePage === i }]"
          @click="activePage = i"
        >
          <span>Home</span>
          <Button
            type="button"
            icon="pi pi-ellipsis-v"
            @click.stop="(event) => menu[i - 1].toggle(event)"
            aria-haspopup="true"
            :aria-controls="`overlay_menu_${i}`"
          />
          <Menu
            ref="menu"
            :id="`overlay_menu_${i}`"
            :model="items"
            :popup="true"
          />
        </button>
      </div>
    </div>
    <hr>
  </div>
</template>

<script setup>
  // ------------------------
  // HANDLE PAGE ITEM 'S MENU 
  // ------------------------
  const activePage = ref(1)
  // ------------------------
  // HANDLE PAGE ITEM 'S MENU 
  // ------------------------
  const menu = ref();
  const items = ref([
    {
      label: 'Options',
      items: [
        {
          label: 'Hide',
          icon: 'pi pi-eye',
          command: () => {
            router.push('/introduction');
          }
        },
        {
          label: 'Delete',
          icon: 'pi pi-trash',
          command: () => {
            router.push('/introduction');
          }
        },
        {
          label: 'Edit',
          icon :'pi pi-pen-to-square',
          command: () => {
            router.push('/introduction');
          }
        
        }
      ]
    }
  ]);


</script>

<style lang="scss" scoped>
.project_page{
  margin-inline-start: 250px;
  .pages{
    @include displayFlex($gap : 10px);
    margin-bottom: 25px;
    .page_item{
      background: #e4e4e450;
      color: $mainColor;
      padding: 5px 10px;
      display: flex;
      align-items: center;
      gap: 15px;
      border-radius: 8px;
      transition: 0.3s;
      button{
        background: transparent;
        border: none;
        color: inherit;
        transform: rotate(90deg);
      }
      &:not(.active):hover{
        background: #e4e4e4;
      }
      &.active{
        background: $mainColor;
        color: #fff;
      }
    }
    +hr{
      background: #333;
      height: 3px;
    }
  }
}


</style>
