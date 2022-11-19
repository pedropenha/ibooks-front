<template>
  <section id="cadastroPatrimonio">
    <div class="md:pl-20 md:pr-20 mt-32">
      <nuxt-link to="/patrimonio" class="mb-36"><Button text-button="Voltar" class-button="info"></Button></nuxt-link>
      <div class="div-form__control">
        <form class="form-control">

          <label for="nome" class="label-control label-obrigatorio">Nome patrimonio*</label>
          <input class="input-form" id="nome" v-model="nome">

          <label for="valor" class="label-control label-obrigatorio">Valor patrimonio*</label>
          <input class="input-form" id="valor" v-model="valor" @keyup="moneyMask()">

          <label for="data_compra" class="label-control">Data de compra</label>
          <input type="date" class="input-form" id="data_compra" v-model="data_compra">

          <label for="categoria" class="label-control label-obrigatorio">Categoria*</label>
          <select class="input-form" v-model="categoria">
            <option v-for="{idCategoria, nomeCategoria} in categoriaArr" :key="idCategoria" :value="idCategoria" :selected="idCategoria === categoria">{{nomeCategoria}}</option>
          </select>

          <label for="n_patrimonio" class="label-control label-obrigatorio">Nº Patrimonio*</label>
          <input type="text" class="input-form" id="n_patrimonio" v-model="n_patrimonio">

          <button @click.prevent="enviar_dados" class="primary">Cadastrar patrimonio</button>
        </form>

      </div>
    </div>
  </section>
</template>

<script>
export default {
  data(){
    return{
      itens: '',
      nome: '',
      valor: '',
      data_compra: '',
      categoriaArr: '',
      categoria: '',
      n_patrimonio: '',
      categorias: ''
    }
  },
  methods:{
    moneyMask(){
      console.log(this.valor)
      this.valor = this.valor.replace('.', '').replace(',', '').replace(/\D/g, '')
      const options = {minimumFractionDigits: 2}

      const result = new Intl.NumberFormat('pt-BR', options).format(
        parseInt(this.valor) / 100
      )

      this.valor = "R$ " + result
    }
  },
  created() {
    this.$axios.get('patrimonio/'+this.$route.params.id).then((response) => {
      this.itens = response.data.mensagem;

      this.nome = this.itens.nome_patrimonio
      this.valor = this.itens.valor_patrimonio
      this.data_compra = this.itens.data_aquisicao
      this.categoria = this.itens.idCategoria
      this.n_patrimonio = this.itens.numero_patrimonio

      this.valor = this.valor+""

      this.valor = this.valor.replace('.', '').replace(',', '').replace(/\D/g, '')
      const options = {minimumFractionDigits: 2}

      const result = new Intl.NumberFormat('pt-BR', options).format(
        parseInt(this.valor) / 100
      )

      this.valor = "R$ " + result

    }).catch((e) => {
      window.location.href="/patrimonio"
    })

    this.$axios.get('categoria/').then((response) => {
      this.categoriaArr = response.data.mensagem;
    })
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
