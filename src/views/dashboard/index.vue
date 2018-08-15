<template>
  <div class="dashboard-container">
    <div class="dashboard-text">name:{{name}}</div>
    <div class="dashboard-text">roles:<span v-for='role in roles' :key='role'>{{role}}</span></div>
    <panel-group></panel-group>
    <el-row :gutter="8">
      <el-col :xs="{span: 24}" :sm="{span: 12}" :md="{span: 12}" :lg="{span: 6}" :xl="{span: 6}" style="padding-right:8px;margin-bottom:30px;">
        <map-table :tableData="citys"></map-table>
        
      </el-col>
      <el-col :xs="{span: 24}" :sm="{span: 12}" :md="{span: 12}" :lg="{span: 12}" :xl="{span: 12}" style="margin-bottom:30px;">
        <china-map :cityData="citys"></china-map>
      </el-col>
      <el-col :xs="{span: 24}" :sm="{span: 12}" :md="{span: 12}" :lg="{span: 6}" :xl="{span: 6}" style="margin-bottom:30px;">
        <todo-list></todo-list>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import PanelGroup from'./components/PanelGroup'
import TodoList from './components/TodoList'
import ChinaMap from './components/Map'
import citys from './components/map-data/get-city-value.js'
import MapTable from './components/Maptable'
export default {
  name: 'dashboard',
  data(){
    return{
      citys:citys
    }
  },
  computed: {
    ...mapGetters([
      'name',
      'roles'
    ])
  },
  components:{
    PanelGroup,
    TodoList,
    ChinaMap,
    MapTable
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
.dashboard {
  &-container {
    margin: 12px;
  }
  &-text {
    font-size: 12px;
    line-height: 12px;
  }
}
</style>
