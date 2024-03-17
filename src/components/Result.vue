<template>
  <p>your result is: {{resultBack}}</p>
  <p class="effec">{{effec}}</p>
</template>

<script>
export default {
    props:['resultBack'],
    data(){
        return{
            effec:null
        }
    },
    methods:{
        renderEffect(){
            if(this.resultBack<250){
                this.effec='So quick man'
            }
            else if(this.resultBack<400){
                this.effec='......... Superrrrrrr'
            }else{
                this.effec='So slow. ..........'
            }
        }
    },
    mounted(){
        this.renderEffect()
    }
}
</script>

<style>
    .effec{
        color:rgb(107, 221, 183);
        font-size: 32px;
    }
</style>