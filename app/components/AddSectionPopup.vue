<template>
  <div class="popup">
    <div class="content">
      <button class="pi pi-times close_btn" @click="$emit('handleShowAddSectionPopup')"></button>
      <h4>Section 's Name</h4>
      <div class="input">
        <input type="text" id="name" placeholder="Name">
      </div>
      <button class="main-btn">Submit</button>
    </div>
  </div>
</template>

<script setup>

</script>

<style lang="scss" scoped>
  .popup{
    .content{
      // padding: 20px 0;
    }
  }
</style>