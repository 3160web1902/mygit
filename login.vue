<template>
<div class="login">
    <div class="dengl" ref="setSho">
        <div class="top" ref="login">
            <h2>Log into your account</h2>
            <input type="text" v-model="email" placeholder="Email">
            <input class="pass" v-model="password" type="password" placeholder="Password">
            <router-link to="/Outing" class="act">registered address?</router-link>
            <button @click="registe">登录</button>
            <span class="msg" :style="msgStyle">{{msg}}</span>
        </div>
    </div>
</div>
</template>
<script>
import { setInterval } from 'timers';

export default {
    data(){
        return {
            email:'',
            password:'',
            msg:'',
            msgStyle:''
        }
    },
    created(){
        // if(sessionStorage.getItem('uname')){
        //     this.ename = 'Hello：' + sessionStorage.getItem('uname');
        // }
    },
    methods:{
        registe(){ 
            
            var email = this.email
            var upwd = this.password
            var url = "http://localhost:3000/user/login"
            if(email && upwd ){
                this.axios.get(url,{params:{email,upwd}}).then(result=>{
                        if(result.data.code === 1){
                        this.msg = result.data.msg +'，2秒后跳转';
                        sessionStorage.setItem("uname",result.data.email)
                        sessionStorage.setItem("pid",result.data.id)
                        this.msgStyle="display:block"
                        setTimeout(()=>{
                            this.msg = ''
                            this.msgStyle="display:none"
                            this.$router.go(-1)

                        },2000)
                    }else if(result.data.code === -1){
                        this.msg = result.data.msg
                        this.msgStyle="display:block"
                        setTimeout(()=>{
                            this.msg = ''
                            this.msgStyle="display:none"
                        },2000)
                    }
                 })
            }

        }
    }
    
    
}
</script>

<style scoped>
    .msg{
        position:absolute;
        display:inline-block;
        width:200px;
        height:80px;
        border-radius:7px;  
        background-color:rgba(0,0,0,0.5);
        top:0;left:0;right:0;bottom:0;
        margin:auto;
        color:#fff;
        line-height:80px;
        transition:opcative .5s;
        display:none;
    }
    .dengl{
        position:fixed;
        width:400px;height:350px;
        top:50%;left:50%;
        z-index:30;
        margin-top:-240px;
        margin-left:-250px;
        padding:3rem;
        border-radius:16px;
        background-color:#fff;
        text-align:center;
        box-shadow: 8px 8px 16px 1px,inset -3px -3px 3px 0;
    }
    
    .dengl h2{
        margin-top:30px;
        font-size:24px;
        font-weight:bold;
    }
    .dengl input{
        width:80%;height:3rem;
        padding-left:60px;
        border-radius:50px 50px;
        margin-top:30px;
        font-size:14px; 
        outline: none; 
        border:1px solid #999;
        background:url("../assets/email.png") no-repeat 2% 50%;
        background-size: 40px; 
    }
    .act:hover{
        color:crimson;
    }
    input.pass{
        background-image:url("../assets/password.png");
    }
    .top a{
        display: inline-block;
        color:#000;
        font-weight: 600;
        font-size:14px;
        margin-top:1rem;
    }
    .dengl button{
        margin-top:2rem;
        width:100%;height:3rem;
        text-align:center;
        line-height:3rem;
        outline: none;
        border:0;
        font-size:18px;
        border-radius:50px 50px;
        background-color:blue;
        color:#fff;
    }
    .dengl button:hover{
        opacity: 0.7;
    }
    .dengl input:focus{
        border-width:2px;
    }
    
    
    @media screen and (max-width:587px){
        .dengl{ 
            margin:0;
            left:0;
            top:100px;
            margin-left:-10px;
            width:80%; 
        }
    }
</style>
