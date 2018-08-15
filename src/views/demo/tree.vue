<template>
  <div class="app-container">
    <el-input placeholder="筛选" v-model="filterText" style="margin-bottom:30px;"></el-input>
   
    <el-row :gutter="12">
      <el-col :xs="{span: 24}" :sm="{span: 12}" :md="{span: 12}" :lg="{span:6}" :xl="{span: 6}" style="padding-right:8px;margin-bottom:30px;">
         <el-tree @current-change="handleClick" class="filter-tree" :data="data2" :props="defaultProps" default-expand-all :filter-node-method="filterNode" ref="tree2"></el-tree>
      </el-col>
      <el-col :xs="{span: 24}" :sm="{span: 12}" :md="{span: 12}" :lg="{span: 18}" :xl="{span: 18}" style="margin-bottom:30px;">
        <el-form ref="form" :model="form" label-width="80px">
          <el-form-item label="父级">
            <el-select v-model="form.label" placeholder="请选择父级">
              <el-option label="区域一" value="shanghai"></el-option>
              <el-option label="区域二" value="beijing"></el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="名称">
            <el-input v-model="form.label"></el-input>
          </el-form-item>
          <el-form-item label="匹配路径">
            <el-input v-model="form.label"></el-input>
          </el-form-item>
          </el-form>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  watch: {
    filterText(val) {
      this.$refs.tree2.filter(val)
    }
  },

  methods: {
    filterNode(value, data) {
      if (!value) return true
      return data.label.indexOf(value) !== -1
    },
    handleClick(data,node){
      console.log(data,node)
      this.form.id=data.id
      this.form.label=data.label
    }
  },

  data() {
    return {
      filterText: '',
      form:{
        id:"",
        label:""
      },
      data2: [{
        id: 1,
        label: '权限管理',
        children: [{
          id: 3,
          label: '角色管理',
        },{
          id: 4,
          label: '菜单管理',
        },
        {
          id: 5,
          label: '用户管理',
        }]
      }, {
        id: 2,
        label: '个人中心'
      }],
      defaultProps: {
        children: 'children',
        label: 'label'
      }
    }
  }
}
</script>

