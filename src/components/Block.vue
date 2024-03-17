<template>
  <div class="block" v-if="mountData" @click="endCount">Click me</div>
</template>

<script>
export default {
    props:['randTime'],
    data(){
        return{
            mountData:false,
            timer:null,
            resultVal:0
        }
    },
    mounted(){
        setTimeout(()=>{
            console.log('mounted')
            this.start()
            this.mountData=true
        },this.randTime)
    },
    updated(){
        console.log('update')
    },
    methods:{
        start(){
            this.timer=setInterval(()=>{
                this.resultVal+=10
            },10)
        },
        endCount(){
            clearInterval(this.timer)
            console.log(this.resultVal)
            this.$emit('endgame',this.resultVal)
        }
    }
}
</script>

<style>
    .block{
        display: flex;
        width: 400px;
        height: 200px;
        justify-content: center;
        align-items: center;
        background-color: rgb(107, 221, 183);
        margin:20px auto;
        cursor:pointer;
    }
</style>