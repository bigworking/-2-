<template>
<div class="reg">
        <div class="fig">欢迎来到登录页面</div>
        <!-- <form action="http://172.16.8.232:8080/denglu"> -->
        <div class="zh">
            <input type="text" name="userName" autocomplete="on" v-model="userName" placeholder="  账号" style="width:448px;height:47px;">
        </div>
        <div class="mm">
            <input type="password" name="passWord" autocomplete="on" v-model="passWord" placeholder="  密码" style="width:448px;height:47px;">
        </div>
        <div class="dl">
            <!-- <router-link :to="{ path: '/repairpeople'}">
                <button class="dlan" type="primary"> -->
                <button class="dlan" type="primary" @click="loginHandle">
                    登录
                </button>
                <!-- </button> -->
            <!-- </router-link> -->
        </div>
        <!-- </form> -->
    </div>
</template>

<script>
// import {mapState,mapMutations,mapAction } from 'vuex'
export default {
    data(){
        return{
            userName:'',
            passWord:'',
            // userToken:'',
        }
    },
    methods:{
        loginHandle(){
            if (this.userName === '' || this.passWord === '') {
                alert('账号或密码不能为空');
            } else {
                this.$http.get('http://127.0.0.1:8080/blog_war/regidter/login?username='+this.userName+'&password='+this.passWord).then(res=>{
                    if(res.body === '' || res.body === null || res.body === undefined){
                        alert('账号或密码错误');
                    }else{
                        if(res.body.userid === 1){
                            this.$router.push('/admin');
                            alert('登陆成功');
                        } else if (res.body.userid === 2){
                            this.$router.push('/repairpeople');
                            alert('登陆成功');
                        } else if (res.body.userid === 3){
                            this.$router.push('/protectpeople');
                            alert('登陆成功');
                        } else {
                            alert('账号或密码错误');
                        }
                    }
                })
            }
        }
    }
}
</script>

<style>
/* .reg{
    background-image:url("../pic/bg.png");
} */
.reg{
    background:url("../pic/bg.png") no-repeat center center;
    background-size:cover;
    background-attachment:fixed;
    position: fixed;
    top: 0px;
    right: 0px;
    width: 100%;
    height: 100%;
    /* margin: 0px;
    padding:0px; */
}
.fig{
    font-size: 46px;
    margin-top: 300px;
    height: 40px;
    font-weight: bold;
    color:#EEEEEE;
}
.zh{
    margin-top: 50px;
}
.mm{
    margin-top: 20px;
}
.dl{
    margin-top: 20px;
}
.dlan{
    width: 450px;
    height: 40px;
    border-radius: 6px;
    background-color: #6495ED;
    color: white;
    font-size: 14px;
    cursor:pointer;
}
input:-webkit-autofill, textarea:-webkit-autofill, select:-webkit-autofill {
    background-color: rgb(189, 255, 238);
    background-image: none;
    color: rgb(0, 0, 0);
}
</style>