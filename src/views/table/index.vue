<template>
  <div class="app-container">
    <div class="table">
      <el-table :data="list" v-loading="listLoading" element-loading-text="Loading"  :height="450" border  highlight-current-row>
      <el-table-column align="center" label='ID' :resizable="false">
        <template slot-scope="scope">
          {{scope.$index+1}}
        </template>
      </el-table-column>
      <el-table-column label="Title" >
        <template slot-scope="scope">
          {{scope.row.title}}
        </template>
      </el-table-column>
      <el-table-column label="Author"  align="center" :resizable="false">
        <template slot-scope="scope">
          <span>{{scope.row.author}}</span>
        </template>
      </el-table-column>
      <el-table-column label="Pageviews"  align="center" :resizable="false">
        <template slot-scope="scope">
          {{scope.row.pageviews}}
        </template>
      </el-table-column>
      <el-table-column class-name="status-col" label="Status" align="center" :resizable="false">
        <template slot-scope="scope">
          <el-tag :type="scope.row.status | statusFilter">{{scope.row.status}}</el-tag>
        </template>
      </el-table-column>
      <el-table-column align="center" prop="created_at" label="Display_time" :resizable="false" width="180">
        <template slot-scope="scope">
          <i class="el-icon-time"></i>
          <span>{{scope.row.display_time}}</span>
        </template>
      </el-table-column>
    </el-table>
    </div>
    <div class="pg">
      <el-pagination
        background
        layout="prev, pager, next"
        :total="total">
      </el-pagination>
    </div>
    
  </div>
</template>

<script>
import { getList } from '@/api/table'

export default {
  data() {
    return {
      list: null,
      listLoading: true,
      total:1
    }
  },
  filters: {
    statusFilter(status) {
      const statusMap = {
        published: 'success',
        draft: 'gray',
        deleted: 'danger'
      }
      return statusMap[status]
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    fetchData() {
      this.listLoading = true
      getList(this.listQuery).then(response => {
        this.list = response.data.items
        this.listLoading = false
        this.total = response.data.items.length
      })
    }
  }
}
</script>
<style scoped>
.pg{
  margin: 0 auto;
  margin-top:20px;
}
.app-container{
  padding-bottom: 0;
}

</style>
