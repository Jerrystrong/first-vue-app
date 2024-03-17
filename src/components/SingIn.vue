<template>
  <div class="container">
    
    <div class="singInContainer">
        <span class="btn-close" @click="closeCreate">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-x" viewBox="0 0 16 16">
                <path d="M4.646 4.646a.5.5 0 0 1 .708 0L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 0 1 0-.708z"/>
            </svg>
        </span>
        <form @submit.prevent="sendForm">
            <h1>S'inscription</h1>
            <input type="text" id="nom" placeholder="Entrer votre nom" v-model="nom" /> 
            <!-- @input="dltError(e,this.nomError)" -->
            <label class="errorMessage" v-if="nomError">{{nomError}}</label>
            <input type="date" id="dateNais" v-model="dateNaissance"/>
            <label class="errorMessage" v-if="dateError">{{dateError}}</label>
            <select name="sexe" id="sexe" v-model="sexe">
              <option value="homme">Man</option>
              <option value="femme">Woman</option>
            </select>
            <input type="text" id="comptenses" placeholder="Entrer vos competences cliquer alt + `,` " v-model="temporalCompetance" @keyup.alt="addComp"/>
            <div class="skills">
              <div v-for="competance in competances" :key="competance" class="skill">
                <div class="bull"></div>
                {{competance}}
              </div>
            </div>
            <input type="email" id="email" placeholder="Entrer votre email" v-model="email"/>
            <label class="errorMessage" v-if="emailError">{{emailError}}</label>
            <input type="password" id="password" placeholder="Creer votre password" v-model="password"/>
            <label class="errorMessage" v-if="passwordError">{{passwordError}}</label>
            <input type="password" id="configPassword" placeholder="Valider votre password" v-model="configPassword"/>
            <label class="errorMessage" v-if="configPasswordError">{{configPasswordError}}</label>
            <button type="submit">Creer un compte</button>
            <label>Ou vous connectez avec</label>
            <div class="social">
                <span class="googleConnection">
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-google" viewBox="0 0 16 16">
                        <path d="M15.545 6.558a9.42 9.42 0 0 1 .139 1.626c0 2.434-.87 4.492-2.384 5.885h.002C11.978 15.292 10.158 16 8 16A8 8 0 1 1 8 0a7.689 7.689 0 0 1 5.352 2.082l-2.284 2.284A4.347 4.347 0 0 0 8 3.166c-2.087 0-3.86 1.408-4.492 3.304a4.792 4.792 0 0 0 0 3.063h.003c.635 1.893 2.405 3.301 4.492 3.301 1.078 0 2.004-.276 2.722-.764h-.003a3.702 3.702 0 0 0 1.599-2.431H8v-3.08h7.545z"/>
                    </svg>
                </span>
            </div>
            <div>
              <!-- Result<br>
              nom:{{nom}}<br>
              date:{{dateNaissance}}<br>
              sexe:{{sexe}}<br>
              comp:{{temporalCompetance}}<br>
              email:{{email}}<br>
              password:{{password}}<br>
              configPassword:{{configPassword}}<br> -->
              <!-- competances:{{competances}} -->
            </div>
        </form>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      nom:'',
      dateNaissance:'',
      sexe:'homme',
      temporalCompetance:'',
      competances:[],
      email:'',
      password:'',
      configPassword:'',
      nomError:'',
      emailError:'',
      passwordError:'',
      configPasswordError:'',
      dateError:'',
      formDat:''
    }
  },
    methods:{
        closeCreate(){
            console.log('closeCreate')
            this.$emit('closeCreate')
        },
        addComp(e){
          // console.log(e)
          // console.log(this.temporalCompetance)
          if(e.key==="," && this.temporalCompetance){
            if(!this.competances.includes(this.temporalCompetance)){
              this.competances.push(this.temporalCompetance)
            }
            this.temporalCompetance=''
            // console.log(this.competances)
          }
        },
        // dltError(e,val){
        //   console.log(val,'val ')
        //   console.log(e,'e val')
        //   e='bob'
        //   val=''
        // },
        sendForm(){
          this.$emit('verifOne')
          setTimeout(()=>{
            if(this.nom.trim()===""){
            this.nomError='Le nom est obligatoire'
            this.$emit('verifTwo','some Error')
            console.log(new Date(this.dateNaissance))
            }else if(this.email.trim()===''){
              this.$emit('verifTwo','some Error')
              this.emailError='Le email est obligatoire';this.nomError='';
            }
            else if(this.password.trim()===''){
              this.$emit('verifTwo','some Error')
              this.passwordError='Le password est obligatoire';this.emailError=''}
            else if(this.configPassword.trim()===''){
            this.$emit('verifTwo','some Error')
            this.configPasswordError='Le password est obligatoire';this.passwordError=''}
            else{
              if(!(this.password===this.configPassword)){
                this.passwordError='Verifier votre mot de passe'
                this.configPasswordError='Verifier votre mot de passe'
                this.$emit('verifTwo','some Error')
              }else if(!(this.email.includes('@'))){
                this.passwordError=''
                this.configPasswordError=''
                this.emailError='Le email est incorrect'
                this.$emit('verifTwo','some Error')
              }
              else{
                const date=new Date(this.dateNaissance)
                const d=new Date()
                if(date.getFullYear()>d.getFullYear()){
                 this.$emit('verifTwo','some Error')
                 this.dateError='la date n\'est pas reel elle se retrouve dans le future'
                }else if((d.getFullYear()-date.getFullYear())<3){
                  this.$emit('verifTwo','some Error')
                  this.dateError='vous n\'avait pas droit a l\'acces car votre age ne convient pas'
                }else{
                  this.$emit('verifTwo','Succes')
                  localStorage.setItem('user',this.nom)
                  const formD={
                    'nom':this.nom,
                    'email':this.email,
                    'password':this.password,
                    'field': this.competances,
                    'datenais':this.dateNaissance,
                    'sexe':this.sexe
                  }
                  this.formDat=formD
                  fetch("data.json",{
                    method:"POST",
                    headers:{
                      "Content-Type":"Application/Json"
                    },
                    body:JSON.stringify(this.formDat)
                  })
                  // then(respons=>respons.json())
                  // then(mes=>console.log(mes))
                  // catch((error)=>console.log(error))
                }
              }
            }
          },2000)
          
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
        overflow:scroll;
        /* padding: 50px 0 ; */
    }
    .singInContainer{
        display: flex;
        flex-direction: column;
        align-items:center ;
        justify-content: center;
        background: white;
        padding:20px;
        border-radius: 10px;
        margin:250px 0px 30px 0px!important;
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
    input,select{
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
    .skills{
      display:flex;
      gap:20px;
      flex-wrap: wrap;
    }
    .skill{
      background-color:rgb(107, 221, 183) ;
      padding:5px 15px;
      border-radius:10px;
      display:flex;
      gap:5px;
      align-items: center;
    }
    .bull{
      display:inline-block;
      border:1px solid white;
      border-radius:50%;
      width:10px;
      height:10px;
      background-color:white;
    }
    .errorMessage{
      color:#ee1200;
      align-self: flex-start;
      text-align: left;
      font-weight: bold;
    }
</style>