<template>
    <div>
        <div class='msg'>
            <h2 @click="handleClick" class="login">{{login}}</h2>
            <span @click="handleP">{{span}}</span>
        </div>
        <div class="navbox clearfix" ref="blocks">
            <div class="nav" ref="nav">
                <nav-pro class="remove navPro" :class="!act?'show bg':''"></nav-pro>
            </div>
            <em :class="act?'icon-daohangtubiaoshouqi':'icon-x'" class="wallow iconfont"  @click="active"></em>
        </div>
    </div>
</template>
<script>
import navPro from './navPro'
import login from './login'
export default {
    data(){
        return {
            act:true,
            bg:false,
            login:'Log in',
            span:'注册'
        }
    },
    computed:{
        getSpan(){
            return this.span
        }
    },
    watch:{
        '$route' (to,form){
            if(sessionStorage.getItem('uname')){ 
                this.login = sessionStorage.getItem('uname')
                this.span='注销'
            }
        }
    },
    methods: {
        handleP(){
            if(this.span === '注册'){
                this.$router.push('/Outing')
            }else if(this.span === '注销'){
                sessionStorage.removeItem('uname')
                sessionStorage.removeItem('pid')
                this.login = 'Log in';
                this.span = '注册'
            }
        },
        handleClick(){
            if(this.login === 'Log in'){
                this.$router.push('/login')
            }else{
                this.$router.push('/Profile')
            }
        },
        active(){
            var blocl = this.$refs.blocks
            var nav = this.$refs.nav
            if(this.act){
                this.act = false;
                this.bg = true;
                blocl.style.display='block';
                nav.style.width="100%";
                // nav.style.display="block";
                nav.style.zIndex=990;

            }else{
                this.act = true;
                this.bg = false;
                blocl.style.height='none';
                nav.style.width="18rem";
                // nav.style.display="none";
                nav.style.zIndex=-1;
            }
        }
    },
    components:{
        navPro,
        login
    }
}
</script>
<style scoped>
    .msg{
        position: relative;
    }
    .login,.msg span{
        position: absolute;
        display:block;
        right:10%;
        top:5%;
        margin-top:3rem;
        font-size:20px;
        font-weight:600;
        border:1px solid #fff;
        padding:1rem 1.5rem;
        color:#fff;
        border-radius:50px 50px;
    }
    .msg span{
        right:5%;
        margin-top:3.7rem;
        font-size:14px;
        padding:.5rem 1rem;
        transition: opacity 1s;
        opacity:0;
    }
    .msg:hover span{
        opacity:1;
    }
    .login:hover,.msg span:hover{
        background-color:rgba(0,0,0,.5);
    }
    [display='none']{
        height:100px;
    }
    [display='block']{
        height:100vh;
    }
    .nav{
        width:18rem;
        height:100%;
        position:fixed;
        z-index:998;
    }
    .navbox{
        width:18rem;
        float:left;
    }
    .wallow{
        display:none;
        font-size:56px;
        width:5rem;
        text-align:center;
        position:absolute;
        top:1rem;right:3rem; 
        z-index: 999;
        color:#fff;
    }
    .show{
        display:block !important;
        background-image:linear-gradient(to top,#00f, #f00);
    }
    .bg{
        background-image:linear-gradient(to top,#00f, #f00);
    }
    @media screen and (max-width:985px){
        .navbox{
            width:100%;
            display:block;
        }
        .wallow{
            display:block;
        }
        .remove{
            display:none;
        }
        .nav{
            z-index: -1;
        }
        .login{
            display:none;
            z-index: -1;
        }
    }
    @media screen and (min-width:986px){
        .nav{
            display:block;
            z-index: -1;
        }
        .login{
            display:block;
        }
    }
</style>

