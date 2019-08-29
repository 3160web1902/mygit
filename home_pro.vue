<template>
<div class="homePro">
    <h2 class="title">Home</h2>
    <div class="home">
        <a href="javascript:;">
            <img src="https://assets.calm.com/d85055f4585f4b0a3b889ce150c963eb.png" alt="">
            <h5>Daily Calm</h5>
            <p>Jun 25 - Little Things</p>
            <i class="iconfont icon-x"></i>
        </a>
    </div>
</div>
</template>
<script>
export default {
    data(){
        return {}
    },
    created(){
        
    }
}
</script>

<style scoped>
.homePro{
  height:100vh;width:100%;
}
    .home{
        margin-left:5rem;
        max-width: 800px;
        width:100%;
        height:94px;
        background-color:#DFECFA;
        border-radius:10px;  
        line-height:10px;
        position:relative;
    }
    .home img{
        width:62px;
        margin-top:18px;
        margin-left:18px;
    }
    .home h5{
        display:inline-block;
        font-size:18px;
        color:#000;
        font-weight:bold;
        position:absolute;
        top:30px;
        left:160px;
    }
    .home p{
        position:absolute;
        font-size:14px;
        top:60px;
        left:160px;
        color:#ccc;
    }
    .home i{
        position:absolute;
        top:62px;
        right:30px;
        margin-top:-18px;
        color:#fff;
    }
    @media screen and (max-width:976px){
        .home{
            /* margin-top:100px; */
            width:93%;
            margin-left:.8rem;
        }
    }
    @media screen and (min-width:977px){
        .home{
            /* margin-top:100px; */
            width:90%;
            margin-left:3rem;
        }
    }
</style>
