<template>
    <div>
        <div style="margin-left:350px;">
            <el-table
            :data="tableData"
            border
            style="width: 100%">
            <el-table-column
            prop="orderno"
            label="维修单号"
            width="150">
            </el-table-column>
            <el-table-column
            prop="ordername"
            label="维修上报人"
            width="150">
            </el-table-column>
            <el-table-column
            prop="repairdevice"
            label="故障设备"
            width="150">
            </el-table-column>
            <el-table-column
            prop="repairpeople"
            label="维修人员"
            width="150">
            </el-table-column>
            <el-table-column
            prop="repairstatus"
            label="维修状态"
            width="150">
            </el-table-column>
            <el-table-column
            label="操作"
            width="180">
            <template slot-scope="scope">
                <el-button @click="handleClick(scope.row)" type="text" size="small">维修说明</el-button>
            </template>
            </el-table-column>
        </el-table>
        </div>
        <div style="margin-left:100px;">
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
        tableData: [
            // {
            //     orderno:'1',
            //     ordername:'a',
            //     repairdevice:'a',
            //     repairpeople:'a',
            //     repairstatus:'1',
            // },
            // {
            //     orderno:'2',
            //     ordername:'b',
            //     repairdevice:'b',
            //     repairpeople:'b',
            //     repairstatus:'2',
            // }
        ],
        total:100,
        currentPage:1,
        pageSize:5,
      }
    },
    created(){
      this.getList();
    },
    methods: {
      getList(){
        this.$http.get('http://127.0.0.1:8080/blog_war/repair/allrepair?crrentPage='+this.currentPage+'&pagesize='+this.pageSize).then(res=>{
          if(res.body !== '' && res.body !== null && res.body !== undefined){
            this.tableData = res.body.maintenances
            this.total = res.body.totalPage
            this.currentPage = res.body.currentPage
          }
          console.log(this.tableData)
        })
      },
      handleSizeChange(pageSize){
          this.pageSize = pageSize
          this.getList()
      },
      handleCurrentChange(currentPage){
          this.currentPage = currentPage
          this.getList()
      },
      handleClick(row) {
        this.$router.push({name:'repairwrite',query:{orderno:row.orderno}})
      },
      // handleSc(row) {
      //   // this.$router.push({name:'look',query:{orderNo:row.orderNo}})
      // }
    },
  }
</script>