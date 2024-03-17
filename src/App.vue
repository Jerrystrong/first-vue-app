<template>
  <h1>
    Game on vue Project One <button class="btn-contact" @click="connectionToggle" v-if="showBtnCon">Connection</button> 
    <span v-if="userConnected" class="user-cont">{{user}} <span class="bull"></span></span>
  </h1>
  <button @click="showBlock" :disabled="disable">Play</button>
  <Block v-if="isPlaying" :randTime="randTime" @endgame="endgame"/>
  <Result v-if="secondPoint" :resultBack="resultBack"/>
  <singUp v-if="singUpPlace" @closeCon="connectionToggle" @createComp="createComp"/>
  <SingIn v-if="singInPlace" @closeCreate="closeCreate" @verifOne="verifOne" @verifTwo="verifTwo"/>
  <CheckResult v-if="checkConnection" :checkConnectionMes="checkConnectionMes"/>
  <!-- <p v-if="secondPoint"> your result is: {{resultBack}}</p> -->

</template>

<script>
import Block from './components/Block.vue'
import Result from './components/Result.vue'
import singUp from './components/singUp.vue'
import SingIn from './components/SingIn.vue'
import CheckResult from './components/CheckResult.vue'
export default {
  name: 'App',
  components: {
    Block,Result,singUp,SingIn,CheckResult
  },
  data(){
    return{
      randTime:null,
      isPlaying:false,
      disable:false,
      resultBack:null,
      secondPoint:false,
      singUpPlace:false,
      singInPlace:false,
      checkConnection:false,
      checkConnectionMes:'',
      showBtnCon:true,
      userConnected:false,
      user:''
    }
  },
  mounted(){
    if(localStorage.getItem('user')){
      this.user=localStorage.getItem('user')
      this.showBtnCon=false
      this.userConnected=true
    }
  },
  methods:{
    showBlock(){
      this.randTime=2000+ Math.random()*5000
      this.isPlaying=true
      this.secondPoint=false
      this.disable=true
      console.log(this.randTime)
    },
    endgame(result){
      this.secondPoint=true
      this.isPlaying=false
      this.resultBack=result
      this.disable=false
    },
    // cote form
    connectionToggle(){
      this.singUpPlace=!this.singUpPlace
    },
    createComp(){
      this.singUpPlace=false
      this.singInPlace=true
    },
    closeCreate(){
      this.singInPlace=false
    },
    // sing verification form
    verifOne(){
      this.checkConnection=true
    },
    verifTwo(mess){
      this.checkConnectionMes=mess
      setTimeout(()=>{
        if(mess==='Succes'){
          this.singInPlace=false
          this.showBtnCon=false
          this.userConnected=true
          this.user=localStorage.getItem('user')
        }
        this.checkConnection=false
        this.checkConnectionMes=''
      },1000)
    }
  }
}
</script>

<style>
h1{
  display:flex;
  justify-content: center;
  align-items:center;
  gap:20px;
}
h1 button{
  background:white ;
  border:1px solid rgb(107, 221, 183);
  font-weight: 600;
  border-radius:10px;
  padding:10px 20px;
  color:rgb(107, 221, 183);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
button{
  background:rgb(107, 221, 183);
  padding:10px 20px;
  border:none;
  border-radius:10px;
  cursor:pointer;
}
button[disabled]{
  cursor:not-allowed;
  background:rgba(107, 221, 183, 0.616);
}
.user-cont{
  padding:10px 20px;
  font-size:12px;
  border:1px solid rgba(107, 221, 183, 0.616);
  display:flex;
  align-items:center;
  gap:20px;
  border-radius:10px;
}
.bull{
  display:block;
  width:10px;
  height:10px;
  border-radius:50%;
  background:rgba(107, 221, 183, 0.616);
}
</style>
