<template>
<div class="Scenes">
    <h2 class="title">ranking list</h2>
    <div class="boxMeditate">
        <a title="双击播放" class="flex-a" href="javascript:;" v-for="(item,i) of list" :key="i">
            <img :src="item.pic_big" alt="" @click="audio(item.song_id,i)">
            <span>{{item.author}}</span>
            <p>{{item.title}}</p>
            <audio ref="rads" :src="myAudio">
            </audio>
        </a>
    </div>
</div>
</template>
<script>
export default {
    data(){
        return {
            list:[],
            myAudio:null
        }
    },
    methods:{
        audio(e,i){
            var isNot = true;
                var url = `http://tingapi.ting.baidu.com/v1/restserver/ting?method=baidu.ting.song.play&songid==${e}`
                this.$jsonp(url).then(result =>{
                if(result.error_code == 22000){
                        this.myAudio = result.bitrate.file_link;
                    }
                })
                this.$refs.rads[i].play();
                isNot = false;
        } 
    },
    created(){
        //搜索：  method=baidu.ting.search.catalogSug&query=海阔天空
        // 播放： method=baidu.ting.song.play&songid=877578
        this.$jsonp('http://tingapi.ting.baidu.com/v1/restserver/ting?method=baidu.ting.billboard.billList&type=25&size=100&offset=0').then(result => {
        this.list = result.song_list;
    })              

    }
}
</script>

<style scoped>
    .Meditate{
        width:100%;
    }
    .boxMeditate{
        padding:1rem;
        width:100%;
        text-align:center;
    }
    .flex-a{
        display:inline-block;
        width:200px;height:240px;
        position:relative;
        border-radius:16px;
        overflow: hidden;
        margin:0 1rem 1rem 0 ;
    }
    .flex-a img{
        width:100%;height:100%;
        transition:transform .5s;
    }
    .flex-a img:hover{
        transform: scale(1.2);
    }
    .flex-a span{
        display:inline-block;
        padding:10px;
        height:12px;
        line-height: 12px;
        background-color:rgba(0,0,0,.7);
        border-radius:50px 50px;
        color:rgba(255,255,255,.8);
        position:absolute;
        top:1rem;
        left:1rem;
    }
    .flex-a p{
        display:block;
        position:absolute;
        bottom: 0;
        height:3rem;
        width:100%;
        background-color:rgba(0,0,0,.7);
        color:#fff;
        line-height: 3rem;
        text-align:center;
        font-size: 14px;
    }
    @media screen and (max-width:528px){
        .boxMeditate{
            padding:0;
            text-align:center;
        }
        .flex-a{
            margin-left:4px;
        }
    }
</style>