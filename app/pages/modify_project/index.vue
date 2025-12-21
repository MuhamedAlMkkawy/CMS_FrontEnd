<template>
  <div class="page modify_project_page">
    <div class="container modify_project_content">
      <VeeForm 
        :validation-schema="modifyProjectSchema" 
        class="form" 
        @submit="handleSubmit"
        v-slot="{ meta }"
        >
        <label for="upload_img" class="upload_image_icon image">
          <img v-if="image.url" :src="image.url" alt="project image" loading="lazy">
          <i v-else class="pi pi-upload"></i>
        </label>
        <label for="upload_img">Upload Logo</label>
        <input type="file" accept="image/*" @change="handleUploadImage($event.target.files[0])" id="upload_img" hidden/>
        <div class="inputs">
          <CustomField 
            name="ar_name"
            type="text"
            placeholder="Project Name in Arabic"
          />
          <CustomField 
            name="en_name"
            type="text"
            placeholder="Project Name in English"
          />
        </div>
        <div class="inputs">
          <CustomTextarea 
            name="ar_description"
            placeholder="Project Description in Arabic"
            :rows="10"
          />
          <CustomTextarea 
            name="en_description"
            placeholder="Project Description in English"
            :rows="10"
          />
        </div>
        <button class="main-btn">Submit</button>
      </VeeForm>
    </div>
  </div>
</template>

<script setup>
  import { modifyProjectSchema } from "../../schemas/modifyProject";

  // HADNLE THE BODY OF THE 
  const image = ref({
    file : null ,
    url : null
  });

  const handleUploadImage = (file) => {
    image.value.file = file;
    image.value.url = URL.createObjectURL(file);
  };



  const handleSubmit = (values) => {
    const formData = new FormData();
    formData.append('image', image.value.file);
    formData.append('ar_name', values.ar_name);
    formData.append('en_name', values.en_name);
    formData.append('ar_description', values.ar_description);
    formData.append('en_description', values.en_description);

    console.log(formData)
  };
</script>
<style lang="scss" scoped>
  .modify_project_page{
    .modify_project_content{
      min-height: 100vh;
      @include displayFlex();
      .form{
        max-width: 992px;
        width: 100%;
        .upload_image_icon{
          @include displayFlex();
          margin: 0 auto 20px;
          @include circle(150px);
          border: 1px solid $mainColor;
          cursor: pointer;
          z-index: 3;
          transition: 0.3s;
          i{
            color: $mainColor;
            font-size: 30px;
          }
          img{
            transition: 0.3s;
            object-fit: contain;
            &:hover{
              filter: brightness(0.7);
            }
          }
          &:hover{
            background: $mainColor;
            i{
              color: #fff;
            }
          }
          + label{
            display: block;
            margin-bottom: 50px;
            color: $mainColor;
            text-align: center;
          }
        }

        .inputs{
          width: 100%;
        }
      }
    }
  }
</style>
