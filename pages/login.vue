<template>
  <section
    class="w-screen h-screen overflow-hidden flex items-center justify-center bg-[url('~/assets/images/Fundo.svg')] bg-no-repeat bg-cover bg-center">
    <!--<div>
      <h1 class="">Login</h1>
    </div> -->
    <div class="h-[45%] w-[28%] bg-white rounded-md ">
        <span class="grid">
          <img src='~/assets/images/Logo.svg' class='w-44 justify-self-center -my-4'></img>
        <form @submit.prevent="logar" class="justify-self-center ">
          <input id="cpf" v-model="cpf" placeholder=" CPF" type="text" @keyup="recebeCPF(cpf)" maxlength="11"
                 class="border-2 border-gray-300 rounded h-10 w-80">
          <br/><br/>
          <input id="senha" v-model="senha" placeholder=" Senha" type="password"
                 class="border-2 border-gray-300 rounded h-10 w-80">
          <br/><br/>
          <button @click.prevent="logar()" class="bg-[#4F46E5] text-white h-10 w-80 rounded justify-self-center">Fazer login</button>
          <br/><br/>
          <a href="#" class="text-[#4F46E5]">Primeiro acesso?</a>
        </form>
      </span>
    </div>

  </section>
</template>

<script>
export default {
  name: 'Login',
  data() {
    return {
      cpf: '',
      senha: ''
    }
  },
  methods: {
    logar() {
      this.cpf = this.cpf.replace(".", "")
      this.cpf = this.cpf.replace(".", "")
      this.cpf = this.cpf.replace("-", "")
      console.log(this.cpf)
      this.$axios.post('/login/', {cpf: this.cpf, senha: this.senha}).then((response) => {
        localStorage.setItem('usuario', JSON.stringify(response.data.mensagem))
        window.location.href = '/patrimonio'
      }).catch((e) => {
        console.log(e)
      })
    },
    recebeCPF(cpf) {
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
    if(localStorage.getItem('usuario') !== null)
    {
      window.location.href = "/patrimonio"
    }
  }
}
</script>

<style>
.button-primary {
  @apply bg-indigo-500;
}

.button-success {
  @apply bg-green-500
}
</style>
