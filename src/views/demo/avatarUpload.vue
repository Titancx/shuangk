<template>
    <div class="avatar-upload">
        <pan-thumb :image="imgDataUrl"></pan-thumb>
        <el-button type="primary" 
        icon="upload" 
        style="position: absolute;top: 15px;margin-left: 40px;" 
        @click="toggleShow">更换头像
        </el-button>
        <my-upload 
        field="img" 
        @crop-success="cropSuccess" 
        @crop-upload-success="cropUploadSuccess"
         @crop-upload-fail="cropUploadFail" 
         v-model="show" 
         :width="300" 
         :height="300" 
         url="/upload" 
         :params="params" 
         :headers="headers" 
         img-format="png">
         </my-upload>
        
    </div>
</template>
<script>
import myUpload from "vue-image-crop-upload";
import PanThumb from '@/components/PanThumb'
export default {
  name: "avatarUpload",
  data() {
    return {
      show: false,
      params: {
        token: "12345",
        name: "avatar"
      },
      headers: {
        samll: "*_~"
      },
      imgDataUrl: "https://wpimg.wallstcn.com/577965b9-bb9e-4e02-9f0c-095b41417191"
    };
  },
  components: {
    myUpload,
    PanThumb
  },
  methods: {
    toggleShow() {
      this.show = !this.show;
    },
    cropSuccess(imgDataUrl, field) {
      this.imgDataUrl = imgDataUrl;
    },
    cropUploadSuccess(jsonData, field) {
      console.log(jsonData);
      console.log("field: " + field);
    },
    cropUploadFail(status, field) {
      console.log(status);
      console.log("field: " + field);
    }
  }
};
</script>
<style>
.avatar-upload{
    padding:20px;
}
</style>
