<template>
  <div class="app-container">
    <el-form ref="form" :model="form" label-width="60px">
      <el-form-item label="名称">
        <el-input v-model="form.name"></el-input>
      </el-form-item>
      <el-form-item label="地区">
        <el-select v-model="form.region" placeholder="选择你的地区">
          <el-option label="Zone one" value="上海"></el-option>
          <el-option label="Zone two" value="北京"></el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="时间">
        <el-col :span="11">
          <el-date-picker type="date" placeholder="选择日期" v-model="form.date1" style="width: 100%;"></el-date-picker>
        </el-col>
        <el-col class="line" :span="2">-</el-col>
        <el-col :span="11">
          <el-time-picker type="fixed-time" placeholder="选择时间" v-model="form.date2" style="width: 100%;"></el-time-picker>
        </el-col>
      </el-form-item>
      <el-form-item label="开关">
        <el-switch v-model="form.delivery"></el-switch>
      </el-form-item>
      <el-form-item label="类型">
        <el-checkbox-group v-model="form.type">
          <el-checkbox label="赤" name="type"></el-checkbox>
          <el-checkbox label="橙" name="type"></el-checkbox>
          <el-checkbox label="黄" name="type"></el-checkbox>
          <el-checkbox label="绿" name="type"></el-checkbox>
        </el-checkbox-group>
      </el-form-item>
      <el-form-item label="资源">
        <el-radio-group v-model="form.resource">
          <el-radio label="青"></el-radio>
          <el-radio label="蓝"></el-radio>
        </el-radio-group>
      </el-form-item>
      <el-form-item label="文本框">
        <el-input type="textarea" v-model="form.desc"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="onSubmit">创建</el-button>
        <el-button @click="onCancel">取消</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        form: {
          name: '',
          region: '',
          date1: '',
          date2: '',
          delivery: false,
          type: [],
          resource: '',
          desc: ''
        }
      }
    },
    methods: {
      onSubmit() {
        this.$message('submit!')
      },
      onCancel() {
        this.$message({
          message: 'cancel!',
          type: 'warning'
        })
      }
    }
  }

</script>

<style scoped>
  .app-container {
    padding-bottom: 0px;
  }

  .line {
    text-align: center;
  }

  .el-checkbox {
    margin-right: 30px;
    margin-left: 0;
  }

</style>
