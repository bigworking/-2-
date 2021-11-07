<template>
    <div>
        <div style="display:flex;">
            <table align="left" style="margin-left:300px;">
                <tr><td style="width:150px;text-align:right;text-align:justify;text-justify:distribute-all-lines;text-align-last:justify;">维修上报人</td><td><input v-model="ordername" type="text" style="border-radius: 6px;width:450px;height:30px;background:rgba(255, 192, 203, 0);"></td></tr>
                <tr><td style="width:150px;text-align:right;text-align:justify;text-justify:distribute-all-lines;text-align-last:justify;">故障设备</td><td><input v-model="repairdevice" type="text" style="border-radius: 6px;width:450px;height:30px;background:rgba(255, 192, 203, 0);"></td></tr>
                <tr><td style="width:150px;text-align:right;text-align:justify;text-justify:distribute-all-lines;text-align-last:justify;">故障描述</td><td><input v-model="issuedescipt" type="text" style="border-radius: 6px;width:450px;height:30px;background:rgba(255, 192, 203, 0);"></td></tr>
                <tr><td style="width:150px;text-align:right;text-align:justify;text-justify:distribute-all-lines;text-align-last:justify;">维修状态</td><td><input v-model="repairstatus" type="text" style="border-radius: 6px;width:450px;height:30px;background:rgba(255, 192, 203, 0);"></td></tr>
                <tr><td style="width:150px;text-align:right;text-align:justify;text-justify:distribute-all-lines;text-align-last:justify;">维修人员</td><td><input v-model="repairpeople" type="text" style="border-radius: 6px;width:450px;height:30px;background:rgba(255, 192, 203, 0);"></td></tr>
                <tr><td style="width:150px;text-align:right;text-align:justify;text-justify:distribute-all-lines;text-align-last:justify;">维修费用</td><td><input v-model="repairtotal" type="text" style="border-radius: 6px;width:450px;height:30px;background:rgba(255, 192, 203, 0);"></td></tr>
                <tr><td style="width:150px;text-align:right;text-align:justify;text-justify:distribute-all-lines;text-align-last:justify;">维修描述</td><td><input v-model="repairdescipt" type="text" style="border-radius: 6px;width:450px;height:30px;background:rgba(255, 192, 203, 0);"></td></tr>
                <tr><td style="width:150px;text-align:right;text-align:justify;text-justify:distribute-all-lines;text-align-last:justify;">验证描述</td><td><input v-model="descript" type="text" style="border-radius: 6px;width:450px;height:30px;background:rgba(255, 192, 203, 0);"></td></tr>
            </table>
            <p style="margin-top:300px;"></p>
        </div>
        <p style="margin-left:-100px;">
            <el-button type="primary" @click="handleadd" style="margin-left:500px;margin-top:90px;cursor:pointer;">添加</el-button>
        </p>
    </div>
</template>

<script>
export default {
    data(){
        return{
          ordername:'',
          repairdevice:'',
          issuedescipt:'',
          repairstatus:'',
          repairpeople:'',
          repairtotal:'',
          repairdescipt:'',
          descript:'',
        }
    },
    methods:{
        handleadd(){
          let data={
            ordername:this.ordername,
            repairdevice:this.repairdevice,
            issuedescipt:this.issuedescipt,
            repairstatus:this.repairstatus,
            repairpeople:this.repairpeople,
            repairtotal:this.repairtotal,
            repairdescipt:this.repairdescipt,
            descript:this.descript,
          }
          this.$http.post('http://127.0.0.1:8080/blog_war/repair/addrepair',data).then(res=>{
            if(res.bodyText === 'ok'){
              this.$message({
                type: 'success',
                message: '添加成功!'
              });
              this.$router.go(0);
            }else{
              alert('添加失败');
            }
          })
        }
    }
}
</script>