<template>
  <el-table
    :data="tableData"
    height="300"
    border
    style="width: 100%">
    <el-table-column
      prop="name"
      label="地区">
    </el-table-column>
    <el-table-column
      prop="value"
      label="单量">
    </el-table-column>
  </el-table>
</template>

<script>
  export default {
    name:'MapTable',
    props:{
        tableData:Array
    },
    data() {
      return {
        
      }
    }
  }
</script>