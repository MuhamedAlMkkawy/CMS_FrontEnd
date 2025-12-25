<template>
  <div class="popup">
    <div class="content">
      <button class="pi pi-times close_btn" @click="$emit('handleShowAddSectionPopup')"></button>
      <h4>Section 's Name</h4>
      <div class="input">
        <input type="text" id="name" placeholder="Name" v-model="section.name">
      </div>
      <button class="main-btn" @click="$emit('handleAddSection' , section)">Submit</button>
    </div>
  </div>
</template>

<script setup>
  const section = ref({
    name : '',
    layout_items: 1,
    components: [], 
    isDragOver: false,
  })
</script>

<style lang="scss" scoped>

</style>