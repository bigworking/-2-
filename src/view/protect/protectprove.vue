<template>
    <div>
        <div style="margin-left:350px;">
            <el-table
            :data="tableData"
            border
            style="width: 100%">
            <el-table-column
            prop="protectpeople"
            label="保养人员"
            width="150">
            </el-table-column>
            <el-table-column
            prop="protectdescribe"
            label="保养描述"
            width="800">
            </el-table-column>
            <el-table-column
            prop="protectstatue"
            label="是否验证通过"
            width="150">
            <template slot-scope="scope">
                <el-button type="primary" size="small" v-if="scope.row.protectstatue === 3" @click="updateHandle(scope.row.protectno,4)">已通过，点击改为不通过</el-button>
                <el-button type="primary" size="small" v-else @click="updateHandle(scope.row.protectno,3)">未通过，点击改为通过</el-button>
            </template>
            </el-table-column>
        </el-table>
        </div>
        <div style="margin-left:-100px;">
            <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page="currentPage"
                :page-sizes="[5, 10, 20, 50]"
                :page-size="pageSize"
                layout="total, sizes, prev, pager, next, jumper"
                :total="total">
            </el-pagination>
        </div>
    </div>
</template>

<script>
  export default {
    data() {
      return {
        tableData: [],
        total:50,
        currentPage:1,
        pageSize:5,
      }
    },
    mounted(){
      this.getList()
    },
    methods: {
      handleSizeChange(pageSize){
          this.pageSize = pageSize
          this.getList()
      },
      handleCurrentChange(currentPage){
          this.currentPage = currentPage
          this.getList()
      },
      getList(){
        this.$http.get('http://127.0.0.1:8080/blog_war/equipmentMaintenance/findByPage?crrentPage='+this.currentPage+'&pagesize='+this.pageSize).then(res=>{
          if(res.body !== '' && res.body !== null && res.body !== undefined){
            this.tableData = res.body.maintenances
            this.total = res.body.totalPage
            this.currentPage = res.body.currentPage
          }
          console.log(this.tableData)
        })
      },
      updateHandle(id,status){
        this.$http.get('http://127.0.0.1:8080/blog_war/equipmentMaintenance/updateStatus?id='+id+'&status='+status).then(res=>{
          if(res.bodyText === 'ok'){
            alert('更新成功');
            this.getList()
          }else{
            alert('更新失败');
          }
        })
      }
    },
  }
</script>