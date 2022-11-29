<template>
    <section class="w-screen h-screen overflow-hidden flex items-center justify-center bg-white bg-cover bg-center">
      <!--<div>
        <h1 class="">Login</h1>
      </div> -->
      <div class="h-[60%] w-[35%] bg-[#f8f8f8] rounded-md ">
          <span class="grid">
          <form @submit.prevent="" class="justify-self-center pt-5">
            <div>Nome (*)</div>
            <input id="nome" v-model="nome" placeholder=" Ex: José" type="text" class="border-2 border-gray-300 rounded h-10 w-80">
            <div>CPF (*)</div>
            <input id="cpf" v-model="cpf" placeholder=" Ex: 000.000.000-00" @keyup="recebeCPF(cpf)" maxlength="11" type="text" class="border-2 border-gray-300 rounded h-10 w-80">
            <div>Data de nascimento (*)</div>
            <input id="dtNasc" v-model="dtNasc"  type="date"  class="border-2 border-gray-300 rounded h-10 w-80">
            <div>Senha (*)</div>
            <input id="senha" v-model="senha" placeholder=" ********" type="password"  class="border-2 border-gray-300 rounded h-10 w-80">
            <div>Nível de acesso (*)</div>
            <input type="radio" id="nivel0" value="nivel0">
            <label for="nivel0">0 - Cliente </label><br>
            <input type="radio" id="nivel1" value="nivel1">
            <label for="nivel1">1 - Colaborador </label><br>
            <input type="radio" id="nivel2" value="nivel2">
            <label for="nivel1"> - Colaborador </label><br>
            <br/><br/>
            <button @click.prevent="" class="bg-[#58E3C2] text-white h-10 w-52 rounded justify-self-center">
                Criar usuário
            </button>
            <br/><br/>
          </form>
        </span>
      </div>
  
    </section>
  </template>
  
  <script>
  export default {
    name: 'Login',
    data(){
      return{
        cpf: '',
        senha: ''
      }
    },
    methods: {
      recebeCPF(cpf) {
        let elementoAlvo = cpf
        const cpfAtual = cpf
        let cpfAtualizado;
        cpfAtualizado = cpfAtual.replace(/(\d{3})(\d{3})(\d{3})(\d{2})/,
          function (regex, argumento1, argumento2, argumento3, argumento4) {
            return argumento1 + '.' + argumento2 + '.' + argumento3 + '-' + argumento4;
          })
        this.cpf = cpfAtualizado;
      }
    },
    created() {
      if(localStorage.getItem('usuario') === null)
      {
        window.location.href = "/login"
      }
  
      if(JSON.parse(localStorage.getItem('usuario')).nivelAcesso < 1){
        window.location.href = '/livros'
      }
    }
  }
  </script>
  
  <style>
  </style>
  