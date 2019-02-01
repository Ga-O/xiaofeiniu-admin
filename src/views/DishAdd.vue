<template>
  <div class="DishAdd">
    <el-breadcrumb>
      <el-breadcrumb-item to="/main">首页</el-breadcrumb-item>
      <el-breadcrumb-item>菜品管理</el-breadcrumb-item>
      <el-breadcrumb-item>菜品类别</el-breadcrumb-item>
    </el-breadcrumb>
    <br>
    <el-form label-width="100px">
      <el-form-item label="菜品图片：">
        <el-upload class="xfn-uploader" :action="uploadAction" :on-success="doUploadSucc" name="dishImg">
          <img v-if="imageUrl" :src="imageUrl" alt="">
        </el-upload>
      </el-form-item>
    </el-form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      imageUrl: '', //要显示的预览图址
      uploadAction: this.$store.state.globalSettings.apiUrl + '/admin/dish/image', //可处理文件上传的数据API
      formData: {
        title: '',
        imgUrl: '', //菜品图片在服务器上的随机文件名
        price: '',
        detail: '',
        catgoryId: ''
      }
    }
  },
  methods: {
    doUploadSucc(res, file) {
      //文件上传成功后，客户端得到响应消息之后的处理函数
      //res:服务器端返回的响应消息
      //file: 从INPUT[type=file]中读取的第一个上传的文件对象
      //console.log(res);
      this.formData.imgUrl = res.fileName;
      this.imageUrl = URL.createObjectURL(file.raw);
      //把上传的文件编码为DataURL字符串
    }
  }
}
</script>
<style lang="scss">
.xfn-uploader {
  .el-upload {
    border: 1px dotted #aaa;
    border-radius: 3px;
    cursor: pointer;
    width: 250px;
    height: 177px;
    overflow: hidden;
    &:hover {
      border-color:#409eff;
    }
  }
  img {
    max-width: 100%;
  }
}
</style>