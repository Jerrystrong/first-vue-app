<template>
  <div class="container">
    
    <div class="singInContainer">
        <span class="btn-close" @click="closeConnection">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-x" viewBox="0 0 16 16">
                <path d="M4.646 4.646a.5.5 0 0 1 .708 0L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 0 1 0-.708z"/>
            </svg>
        </span>
        <form>
            <h1>Se connecter</h1>
            <input type="email" id="email" placeholder="Entrer votre email"/>
            <input type="password" id="password" placeholder="Entrer votre password"/>
            <button type="submit">Se connecte</button>
            <label>Vous n'avez pas un compte, <a href="" id="createAccount" @click.prevent="createAccount">Creer un compte</a></label>
            <label>Ou vous connectez avec</label>
            <div class="social">
                <span class="googleConnection">
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-google" viewBox="0 0 16 16">
                        <path d="M15.545 6.558a9.42 9.42 0 0 1 .139 1.626c0 2.434-.87 4.492-2.384 5.885h.002C11.978 15.292 10.158 16 8 16A8 8 0 1 1 8 0a7.689 7.689 0 0 1 5.352 2.082l-2.284 2.284A4.347 4.347 0 0 0 8 3.166c-2.087 0-3.86 1.408-4.492 3.304a4.792 4.792 0 0 0 0 3.063h.003c.635 1.893 2.405 3.301 4.492 3.301 1.078 0 2.004-.276 2.722-.764h-.003a3.702 3.702 0 0 0 1.599-2.431H8v-3.08h7.545z"/>
                    </svg>
                </span>
            </div>
        </form>
    </div>
  </div>
</template>

<script>
export default {
    methods:{
        closeConnection(){
            console.log('closeCon')
            this.$emit('closeCon')
        },
        createAccount(){
            this.$emit('createComp')
        }
    }
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
    }
    .singInContainer{
        display: flex;
        flex-direction: column;
        align-items:center ;
        justify-content: center;
        background: white;
        padding:20px;
        border-radius: 10px;
    }
    .btn-close{
        align-self: flex-end;
        color:rgb(107, 221, 183);
        cursor:pointer;
    }
    .btn-close svg{
        width: 32px;
        height: 32px;
    }
    .singInContainer form{
        display: grid;
        width: 300px;
        gap:20px;
    }
    input{
        height: 40px;
        border:1px solid lightgray;
        border-radius: 10px;
        padding-left:20px ;
    }
    label{
        font-size: 12px;
        color:#535353;
    }
    .social{
        display: flex;
        align-items:center ;
        justify-content: center;    
    }
    .googleConnection{
        background-color:rgb(107, 221, 183) ;
        width: 50px;
        height: 50px;
        display: flex;
        align-items: center;
        justify-content: center;
        border-radius: 50%;
    }
</style>