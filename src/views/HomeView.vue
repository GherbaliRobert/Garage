<template>
  <div class="wrapper">
    <div class="box">
      <img class="logoImg" src="../assets/dgss3Lgo.png" alt="">
	<form @submit="handleLogin">
		<span class="text-center">Mecanizare</span>
    <br><br>
	<div class="input-container">
		<input type="text" required="" id="username" v-model="username" />
		<label>Adresa email sau username</label>		
	</div>
	<div class="input-container">		
		<input type="password" required="" id="password" v-model="password"/>
		<label>Parola</label>
	</div>
  <br>
  <span style="color: red">{{ failAuth }}</span>
  <br>
		<button type="button" class="btn" @click="handleLogin">Autentificare</button>
</form>	
</div>
</div>
</template>

<script>
import PrincipalPage from './PrincipalPage.vue';
export default {
  data() {
    return {
      username: '',
      password: '',
      isLoggedIn: false,
      failAuth:''
    };
  },
  methods: {
    handleLogin() {
      // Verifică dacă datele de autentificare sunt valide
      if (this.username === 'utilizator' && this.password === 'parola') {
        console.log('e ok')
        this.isLoggedIn = true;
        // Redirecționează către pagina principală sau altă rută
        this.$router.push('../PrincipalPage');
      } else {
        this.failAuth = "Date de acces incorecte !"
        alert('Nume de utilizator sau parolă incorecte');

      }
    },
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Noto+Sans:400,400i,700,700i&subset=greek-ext');

.text-center{
	color:#fff;	
	text-transform:uppercase;
    font-size: 25px;
    display: block;
    text-align: center;
}
.box{
	position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%,-50%);
    background-color: rgba(0, 0, 0, 0.89);
    border-radius: 3px;
    padding: 35px 50px;
    width: 400px;
}
.input-container{
	position:relative;
	margin-bottom:25px;
}
.input-container label{
	position:absolute;
	top:0px;
	left:0px;
	font-size:16px;
	color:#fff;	
	transition: all 0.5s ease-in-out;
}
.input-container input{ 
  border:0;
  border-bottom:1px solid #555;  
  background:transparent;
  width:100%;
  padding:8px 0 5px 0;
  font-size:16px;
  color:#fff;
}
.input-container input:focus{ 
 border:none;	
 outline:none;
 border-bottom:1px solid rgb(108,4,44);	
}
.btn{
	color:#fff;
	background-color:rgb(108,4,44);
	outline: none;
    border: 0;
    color: #fff;
	padding:10px 20px;
	text-transform:uppercase;
	margin-top:50px;
	border-radius:2px;
	cursor:pointer;
	position:relative;
}
/*.btn:after{
	content:"";
	position:absolute;
	background:rgba(0,0,0,0.50);
	top:0;
	right:0;
	width:100%;
	height:100%;
}*/
.input-container input:focus ~ label,
.input-container input:valid ~ label{
	top:-12px;
	font-size:12px;
	
}

.wrapper {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

body {
  margin: 0;
  background-image: url('../assets/loginImg.jpg');
  background-size: cover;
  background-repeat: no-repeat;
  height: 100%;
  
  width: 100%;
  display: flex;
  justify-content: center;
}

.logoImg{
  margin-bottom: 35px;
  border-radius: 20px;
}
input{
  border-radius: 5px;
  width: 75%;
  height: 25px;
}
</style>