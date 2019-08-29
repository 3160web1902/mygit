<template>
    <div class="box">
        <ul class="navbar">
            <li>
                <router-link to="/home"><em class="iconfont icon-jia"></em>Home</router-link>
            </li>
            <li>
                <router-link to="/Sleep"><em class="iconfont icon-yueliang4"></em>Sleep</router-link>
                </li>
            <li>
                <router-link to="/Meditate"><em class="iconfont icon-yuanxin"></em>Meditate</router-link>
            </li>
            <li>
                <router-link to="/Music"><em class="iconfont icon-yinle"></em>Music</router-link>
            </li>
            <li>
                <router-link to="/Masterclass"><em class="iconfont icon-dengpao"></em>Masterclass</router-link>
            </li>
            <li>
                <router-link to="Body"><em class="iconfont icon-dengpao"></em>Body</router-link>
            </li>
            <li>
                <router-link to="/Scenes"><em class="iconfont icon-shan"></em>Scenes</router-link>
            </li>
            <li>
                <router-link to="/Profile"><em class="iconfont icon-yonghu2"></em>Profile</router-link>
            </li>
            <li>back to calm.com</li>
        </ul>
    </div> 
</template>
<script>
export default {
    data(){
        return {
            Urls : '',
            isNot:true
        }
    }
}
</script>

<style scoped>
    .box{
        border-right:12px solid #fff;
        background-color:rgba(0, 0, 0, .5);
        box-sizing: border-box;
        position:relative;
        z-index: 999;
        width:100%;height:100%;
    }
    a{
        color:#fff;
        font-size:16px;
        font-family: Calibre, "Helvetica Neue", Helvetica, Arial, sans-serif; 
    }
    .navbar li a:hover em{
        background-image:linear-gradient(to right,#00f,#f0f );
    }
    .font{
        font-size:24px;
    }
    .navbar{
        width:100%;
        height:100vh;
        padding-top:5rem;
    }
    .navbar li{
        width:100%;height:4rem;
        line-height:4rem;
        margin-left:1rem;
    }
    .navbar em{
        /* background-image:linear-gradient(to right,#f00,#f0f ); */
        color:#fff;
        border-radius:50%;
        padding:.5rem;
        margin-right:1rem;
    }
    .navbar li:last-child{
        color:#fff;
        font-size:14px;
    }
    .pitch{
        font-weight: bold;
    }
    @media screen and (max-width:976px){
        .box{
            border:0;
        }
    }
</style>
