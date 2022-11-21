<template>
  <section class="w-screen h-screen overflow-hidden flex items-center justify-center bg-white bg-cover bg-center">
    <!--<div>
      <h1 class="">Login</h1>
    </div> -->
    <div class="h-[40%] w-[35%] bg-[#f8f8f8] rounded-md ">
        <span class="grid">
        <form @submit.prevent="" class="justify-self-center pt-5">
          <div>Nome do exemplar (*)</div>
          <input id="nomeEx" v-model="exemp" placeholder=" Ex: gato de botas" type="text" disabled class="border-2 border-gray-300 rounded h-10 w-80">
          <div>Número de série (*)</div>
          <input id="serie" v-model="nSerie" placeholder=" Ex: 132313" type="text" class="border-2 border-gray-300 rounded h-10 w-80">
          <div>CPF do usuário (*)</div>
          <input id="cpf" v-model="cpf" placeholder=" CPF" type="text" @keyup="recebeCPF(cpf)" maxlength="11" class="border-2 border-gray-300 rounded h-10 w-80">
          <br/><br/>
          <button @click.prevent="" class="bg-[#58E3C2] text-white h-10 w-52 rounded justify-self-center">Emprestar exemplar</button>
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
