<template>
<div class="Music">
    <h2 class="title">Music</h2>
    <div class="boxMusic">
        <div class="MusicHead">
            <input class="input" v-model="field" placeholder="请输入搜索内容" type="text">
            <a ref="btn" @click="submit" class="iconfont icon-sousuokuang"> </a>
            <p>{{prompt}}</p>
        </div>
        <div class="left">
            <a class="flex-a" v-for="(item,i) of list" :key="i"  title="双击播放" @click="audio(item.songid,i)">
                <h3>{{item.songname}}</h3>
                <span>{{item.artistname}}</span>
                <audio ref="rads" :src="myAudio"></audio>
            </a>
        </div>
        <div class="right">
            <img :src="myImg" alt="">
        </div>
    </div>
    <ul ref="dff">
        <li v-for="(item,index) of list" :key="index"></li>
    </ul>
</div>
</template>
<script>
export default {
    data(){
        return {
            list:[],
            myAudio:null,
            field:'',
            prompt:'',   //提示文字
            myImg:''
        }
    },
    methods:{
        audio(e,i){
                var url = `http://tingapi.ting.baidu.com/v1/restserver/ting?method=baidu.ting.song.play&songid=${e}`
                this.$jsonp(url).then(result =>{
                    if(result.error_code == 22000){
                        this.myAudio = result.bitrate.file_link;
                        this.myImg = result.songinfo.pic_huge;
                    }
                })
                this.$refs.rads[i].play();
        },
        submit(e,i){
            if(sessionStorage.getItem('uname')){
            var fields = this.field;
            var url = `http://tingapi.ting.baidu.com/v1/restserver/ting?method=baidu.ting.search.catalogSug&query=${fields}`
             this.$jsonp(url).then(result =>{
            
                if(result.error_code == 22000){
                    this.list = result.song
                    this.prompt =  `检索到${result.song.length}条相关数据`
                    this.myImg = ''
                }else{
                    this.prompt = "未检索到相关内容"
                    this.list = []
                     }
                })
            }else{
                this.prompt = "请先登录,2秒后跳转";
                setTimeout(()=>{
                    this.$router.push('/Login');
                },2000)
            }
        }
    },
    created(){
       document.onkeyup=(e)=>{
            if(e.key == 'Enter'){
                if(this.field){
                    this.submit()
                }
            }
            
        }
    },
    mounted(){
        
    }
}
</script>

<style scoped>
    .Music{
        width:100%;
        }
    .boxMusic{
        width:100%;height:50px;
        text-align:center;
        line-height:50px;
        }
    .MusicHead{
            vertical-align: middle;
            position:relative;
        }
    .MusicHead input{
        box-sizing: border-box;
        outline:none;
        display:inline-block;
        background-color:transparent;
        border:2px solid crimson;
        font-size:16px !important;
        font-weight: bold;
        width:320px;height:50px;
        position:absolute;
        right:50%;
        color:crimson;
        margin-right:-140px;
        padding-left:12px;
        border-radius:7px;
        font-size:14px;
        padding-right:50px;
     }

    input::-webkit-input-placeholder, textarea::-webkit-input-placeholder {
     color: rgb(245, 170, 30);
    font-size: 16px;
    font-weight: normal;
    }

    input:-moz-placeholder, textarea:-moz-placeholder {
        color: rgb(245, 170, 30);
        font-size: 16px;
        font-weight: normal;
    }

    input::-moz-placeholder, textarea::-moz-placeholder {
        color: rgb(245, 170, 30);
        font-size: 16px;
        font-weight: normal;
    }

    input:-ms-input-placeholder, textarea:-ms-input-placeholder {
        color: rgb(245, 170, 30);
        font-size: 16px;
        font-weight: normal;
    }

    .MusicHead a{
        color:crimson;
        display: inline-block;
        vertical-align: middle;
        font-size:45px;
        font-weight: 100;
        margin-left:330px;
     }
    .MusicHead p{
        margin:1rem 0;
        color:crimson;
     }
    .MusicHead button:hover{
        color:crimson;
     }
     .left{
         float: left;
         width:50%;height:100%;
     }
     .right{
         float:right;
         width:50%;
         box-sizing:border-box;
         padding:7rem;
     }
     .right img{
         width:100%;height:100%;
     }
    .flex-a{
        display:block;
        width:100%;height:48px;
        position:relative;
        border-bottom:1px dashed #ccc;
        overflow: hidden;
        margin:0 ;
        line-height:48px;
        text-align: left;
    }
    .flex-a:first-child{
        border-top:1px dashed #ccc;
    }
    .flex-a:last-child{
        border-bottom:0;
    }
    .flex-a:hover{
        background-color:rgba(0,0,0,.1);
    }
    .flex-a span{
        display:inline-block;
        color:chocolate;
    }
    .flex-a h3{
        display:inline-block;
        color:#fff;
        font-weight: bold;
        font-size: 14px;
        margin:0 2rem;
    }
    .flex-a button{
        position:absolute;
        top:16px;left:20rem;
        border:0;
        background-color:blueviolet;
        color:cornsilk;
        font-size:12px;
        padding:5px;
    }
    @media screen and (max-width:528px){
        .boxMusic{
            padding:0;
            text-align:center;
        }
        .flex-a{
            margin-left:4px;
        }
        .right{
            display:none;
        }
        .left{
            width:100%;
        }
        .input{
            width:100%;height:2rem;
        }
    }
    
</style>