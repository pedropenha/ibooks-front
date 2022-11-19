<template>
  <section>
    <h1>Login</h1>

    <form @submit.prevent="logar">
      <label for="cpf">CPF:</label>
      <input id="cpf" v-model="cpf">

      <label for="cpf">Senha:</label>
      <input id="cpf" v-model="senha">

      <input type="submit">
    </form>
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
  methods:{
    logar(){
      this.$axios.post('/login/', {cpf: this.cpf, senha: this.senha}).then((response) => {
        console.log(response.data)
      }).catch((e) => {
        console.log(e)
      })
    }
  }
}
</script>

<style>
  .button-primary{
    @apply bg-indigo-500;
  }
  .button-success{
    @apply bg-green-500
  }
</style>
