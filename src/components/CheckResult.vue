<template>
  <div class="container">
    <div class="placeVeri">
        <div class="loader"></div> 
        <div>{{checkConnectionMes}}</div>
    </div>
  </div>
</template>

<script>
export default {
    props:['checkConnectionMes']
}
</script>

<style scoped>
.container{
        background: rgba(3, 3, 3, 0.637);
        position:fixed;
        top:0;
        bottom: 0;
        left: 0;
        right: 0;
        width:100%;
        height:100vh;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
        overflow:scroll;
        /* padding: 50px 0 ; */
    }
    .placeVeri{
        display: flex;
        border-radius: 20px;
        width:300px;
        height: 200px;
        background: white;   
        justify-content: center;
        align-items: center;
        flex-direction: column;
    }
    .loader {
    width: 15px;
    aspect-ratio: 1;
    border-radius: 50%;
    animation: l5 1s infinite linear alternate;
  }
@keyframes l5 {
    0%  {box-shadow: 20px 0 #000, -20px 0 #0002;background: #000 }
    33% {box-shadow: 20px 0 #000, -20px 0 #0002;background: #0002}
    66% {box-shadow: 20px 0 #0002,-20px 0 #000; background: #0002}
    100%{box-shadow: 20px 0 #0002,-20px 0 #000; background: #000 }
}
</style>