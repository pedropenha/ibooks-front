<template>
  <section id="cadastroPatrimonio">
    <NavBar/>
    <div class="md:pl-20 md:pr-20 mt-32">
      <nuxt-link to="/patrimonio" class="mb-36"><Button text-button="Voltar" class-button="info"></Button></nuxt-link>
      <div class="div-form__control">
        <form class="form-control">

          <label for="nome" class="label-control label-obrigatorio">Nome patrimonio*</label>
          <input class="input-form" id="nome" v-model="nome" required>

          <label for="valor" class="label-control label-obrigatorio">Valor patrimonio*</label>
          <input class="input-form" id="valor" v-model="valor" @keyup="moneyMask()" required>

          <label for="data_compra" class="label-control label-obrigatorio">Data de compra*</label>
          <input type="date" class="input-form" id="data_compra" v-model="data_compra" required>

          <label for="categoria" class="label-control label-obrigatorio">Categoria*</label>
          <select class="input-form" v-model="categoria" required>
            <option v-for="({idCategoria, nomeCategoria}, index) in categorias" :key="idCategoria" :value="idCategoria">{{nomeCategoria}}</option>
          </select>

          <label for="n_patrimonio" class="label-control label-obrigatorio">Nº Patrimonio*</label>
          <input type="text" class="input-form" id="n_patrimonio" v-model="n_patrimonio" required>

          <button type="submit" @click.prevent="enviar_dados" class="primary">Cadastrar patrimonio</button>
        </form>

      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "CadastraPatrimonio",
  data(){
    return{
      nome: '',
      valor: '',
      data_compra: '',
      categoria: '',
      n_patrimonio: '',
      categorias: ''
    }
  },
  methods:{
    enviar_dados(){
      this.valor = this.valor.substring(3, this.valor.length)
      this.valor = this.valor.replace(',', '').replace('.', '').replace(/\D/g, '')

      console.log(this.valor)
      this.$axios.post('patrimonio/', {nome: this.nome, valor: this.valor, data_compra: this.data_compra, categoria: this.categoria, numero_patrimonio: this.n_patrimonio})
        .then((response) => {
          if(response.data.status === "sucesso"){
            alert("Item inserido com sucesso voltando a página inicial")
            window.location.href = "/patrimonio"
          }
        }).catch((err) => {
        console.log(e)
      })
    },

    moneyMask(){
      console.log(this.valor)
      this.valor = this.valor.replace('.', '').replace(',', '').replace(/\D/g, '')
      const options = {minimumFractionDigits: 2}

      const result = new Intl.NumberFormat('pt-BR', options).format(
        parseInt(this.valor) / 100
      )

      this.valor = "R$ " + result
    },
  },
  created() {
    this.$axios.get('categoria/').then((response) => {
      this.categorias = response.data.mensagem;
    })

    if(localStorage.getItem('usuario') === null)
    {
      window.location.href = "/login"
    }

    if(JSON.parse(localStorage.getItem('usuario')).nivelAcesso < 1){
      window.location.href = '/patrimonio'
    }
  }
}
</script>

<style scoped>
  .input-form{
    @apply border-gray-400 w-full border-b transition mb-6
  }
  .input-form:hover{
    @apply border-gray-800
  }
  .form-control{
    @apply flex justify-center items-center flex-wrap w-6/12
  }
  .div-form__control{
    @apply w-full flex justify-center
  }
  .label-control{
    @apply w-full mb-2
  }
  .primary{
    @apply bg-green-400 shadow-md shadow-green-300 text-white rounded-md transition p-6;
  }
  .primary:hover{
    @apply bg-green-500 shadow-green-400;
  }
  .label-obrigatorio{
    @apply text-red-900;
  }
</style>
