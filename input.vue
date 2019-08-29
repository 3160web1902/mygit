<template>
<div class="inputBox">
    <h2 class="title">chat room</h2>
    <div class='panel'>
        <span @click="handleClick" class='span'>{{span}}</span>
    </div>
    <div class="left" v-show="!isText">
        <a v-for="(item,index) of arr" :key="index">
            <em>{{item.years}}</em>
            <h1>{{item.title}}</h1>
            <p>{{item.messages}}</p>
        </a>
    </div>
    <div class="right"  v-show="isText">
        <div>
            <input placeholder="标题" v-model="title" type="text">
            <textarea @change="handleChange" v-show="isText" name="texts" id="text" v-model="value" cols="50" rows="10"></textarea>
        </div>
         <button @click="handleText" class='btn'>提交</button>
    </div>
    <span class="msg" :style="msgStyle">{{msg}}</span>
</div>
</template>
<script>
export default {
    data(){
        return {
            list:[],
            value:'',
            isText:false,
            title:'',
            msg:'',
            msgStyle:'',
            span:'写',
            arr:[]
        }
    },
    methods:{
        handleChange(){
            localStorage.setItem('message',this.value)
        },
        handleClick(){
            if(this.isText){
                this.span='读';
                this.isText=false;
            }else{
                this.span='写';
                this.isText=true;
            }
        },
        handleText(){
            if(sessionStorage.getItem('pid')){
                let myDate = new Date()
                if(myDate.getMinutes().toString().length===1){
                    var fen = '0'+myDate.getMinutes()
                    }else{
                        fen = myDate.getMinutes()
                    }
                let times = myDate.getFullYear()+'年'+(myDate.getMonth()+1)+'月'+ myDate.getDate()+'日'+' '+myDate.getHours()+':'+fen
                let pid = sessionStorage.getItem('pid');
                let text = this.value; 
                let title = this.title;
                let url = `http://localhost:3000/user/input?pid=${pid}&messages=${text}&years=${times.toString()}&title=${title}`;
                this.axios.get(url).then(result=>{
                    this.value='';
                    this.title='';
                    this.msg=result.data.msg;
                    this.msgStyle="display:block"
                    setTimeout(()=>{
                    this.msgStyle="display:none"
                    this.msg =''
                        },2000)
                    console.log(result)
                })
            }else{
                this.msgStyle="display:block"
                this.msg  = '你为登录，2秒后跳转到登录界面！'
                setTimeout(()=>{
                    this.$router.push('/login');
                    this.msgStyle="display:none"
                    this.msg =''
                },2000)
            }
        }
    },
    created(){
        if(sessionStorage.getItem('pid')){
            let pid=sessionStorage.getItem('pid');
            let url = `http://localhost:3000/user/message?pid=${pid}`
            this.axios.get(url).then(result=>{
                this.arr = result.data
                console.log(result)
            })
        }

        }
}
</script>

<style scoped>
.btn{
    background-color:transparent;
    border:1px solid #fff;
    border-radius:50px 50px;
    padding:10px;
    color:#fff;
    font-weight: bold;
    margin-top:1rem;
}
.btn:hover,.panel span:hover{
    background-color:rgba(0,0,0,0.5);
    color:#fff;
}
.left{
    text-align:center;
    width:80%;
    background-color:beige;
    box-shadow:5px 5px 5px 0;
    border-radius:3px;
    box-sizing:border-box;
    padding:1rem;
}
.left a em{
    display:block;
    margin-bottom:1rem;
    color:gray;

}
.left a h1{
    font-size:18px;
    font-weight:bold;
}
.left a p{
    font-weight:16px;
    color:#000;
    margin-bottom:2rem;
    margin-top:.5rem;
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
    text-align:center;
    line-height:80px;
    transition:opcative .5s;
    display:none;
    }
.panel span{
    display: inline-block;
    border:1px solid #fff;
    border-radius:50px 50px;
    padding:10px;
    color:#fff;
    font-weight: bold;
    text-align:center;
    line-height:20px;
    margin-bottom:1rem;
}
.right input{
    outline:none;
    background-color:transparent;
    border-bottom:2px solid #fff;
    font-size:20px;
    padding-left:8px;
    color:#fff;
    display:block;
    margin-bottom:3rem;
}
#text{
    background-color:beige;
    font-size:24px;
    border:0;
    }
@media screen and (max-width:976px) {
    .left{width:100% }
}
</style>
