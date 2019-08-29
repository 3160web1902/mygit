<template>
<div class="login">
    <div class="dengl" ref="setSho">
        <div class="top" ref="login">
            <h2>register an account</h2>
            <input type="text" v-model="email" @change="emailText" placeholder="Email">
            <input class="phone" v-model="phone" type="text" @change="phoneText" placeholder="Phone">
            <input class="pass" v-model="password" type="password" @change="upwdText" placeholder="Password">
            <button @click="registe">登录</button>
            <span class="msg" :style="msgStyle">{{msg}}</span>
            <span class="span">{{span1}}</span>
            <span class="span2 span">{{span2}}</span>
            <span class="span3 span">{{span3}}</span>
        </div>
        <router-link to="/Login" class="jiant iconfont icon-arrow-left"></router-link>
    </div>
</div>
</template>
<script>

export default {
    data(){
        return {
            email:'',
            password:'',
            msg:'',
            msgStyle:'',
            phone:'',
            $404:false,
            span1:'',
            span2:'',
            span3:''
        }
    },
    created(){
        // if(sessionStorage.getItem('uname')){
        //     this.ename = 'Hello：' + sessionStorage.getItem('uname');
        // }
    },
    methods:{
        registe(){
            var email = this.email;
            var phone = this.phone;
            var upwd = this.password; 
            var rege = /^[a-zA-Z0-9_-]+@[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+$/
            var regp = /^1([38]\d|5[0-35-9]|7[3678])\d{8}$/;
            var regu = /^\d{6,16}$/;
            if(rege.test(this.email) && regp.test(this.phone) && regu.test(this.password) && this.$404){
               var url = "http://localhost:3000/user/reg";
                this.axios.get(url,{params:{
                email,phone,upwd
                }}).then(result=>{
                //   注册完成后清空
                    this.msg = "注册成功，正在跳转！"
                    this.msgStyle="display:block"
                    // 两秒后切换到登录页面
                setTimeout(()=>{
                    this.$router.push('/Login')
                    this.msgStyle="display:none";
                    },2000)
                })
               
            }else{
                this.msg = "皮 ???"
                this.msgStyle="display:block"
                setTimeout(()=>{
                    this.msg="";
                    this.msgStyle="display:none";
                    },2000)
                
            }

        },
        emailText(){
             var emailText = this.email;
            // 邮箱正则
            var reg = /^[a-zA-Z0-9_-]+@[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+$/
            if(reg.test(emailText)){
                this.axios.get('http://localhost:3000/user/checkemail',{params:{email:emailText}}).then(result=>{
                    if(result.data.code==200){
                      //可以使用
                        this.span1=result.data.msg
                        this.$404 = true;
                    }else{
                        //用户已注册
                        this.span1=result.data.msg;
                        this.$404 =false;
                    }
                })
            }else{
                // 如果错误
                this.email=""
                this.span1='请输入正确的邮箱！' 
                this.$404 =false;
            }
        },
        phoneText(){
            var Text = this.phone;
            // 手机正则
            var reg = /^1([38]\d|5[0-35-9]|7[3678])\d{8}$/;
            if(reg.test(Text)){
                this.span2 = '';
            }else{
                // 如果错误
                this.phone="";
                this.span2 = "无效的手机号！";
            }
        },
        upwdText(){
            var Text = this.password;
            // 密码正则
            var reg = /^\d{6,16}$/
            if(reg.test(Text)){
                this.span3 = '';
            }else{
                // 如果错误
                this.upwd = '';
                this.span3 = '请输入6~16位数字';
                return;
            }
        }
    }
    
    
}
</script>

<style scoped>
    .jiant{
        position: absolute;
        left:7%;top:7%;
        font-size:32px;
    }
    .jiant:hover{
        color:aqua;
    }
    .span{
        position:absolute;
        top:36.5%;left:35%;
        color:#f00;
    }
    .span2{
        top:54.5%;
    }
    .span3{
        top:72.5%;
    }
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
        font-size:14px;
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
    .dengl .phone{
        background-image:url("../assets/phone.png");
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
