<template>
  <section id="darBaixaEmLivro">
    <div class="md:pl-20 md:pr-20 mt-32">
      <nuxt-link to="/livros" class="mb-36">
        <Button text-button="Voltar" class-button="info"></Button>
      </nuxt-link>
      <div class="div-form__control">
        <form class="form-control" @submit.prevent="baixa_livro">
          <label for="motivoBaixa" class="label-control label-obrigatorio">Motivo da baixa*</label>
          <textarea v-model="motivo_baixa" class="input-form" id="motivoBaixa" required></textarea>

          <label for="dataBaixa" class="label-control label-obrigatorio">Data da baixa*</label>
          <input type="date" class="input-form" id="dataBaixa" v-model="data_baixa" required>

          <button type="submit" class="primary">Efetivar baixa</button>
        </form>

      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      exemplar_id: this.$route.params.idExemplar,
      colaborador_id: JSON.parse(localStorage.getItem('usuario')).nivelAcesso,
      motivo_baixa: '',
      data_baixa: '',
    }
  },
  methods: {
    baixa_livro() {
      this.$axios.post('/baixaLivro/', {
        exemplar_id: this.exemplar_id,
        colaborador_id: this.colaborador_id,
        motivo_baixa: this.motivo_baixa,
        data_baixa: this.data_baixa
      }).then((response) => {
        if (response.data.status === 200)
          alert('Livro dado baixa com sucesso, voltando a página de exemplares.')
        window.location.href = "/livros"
      }).catch((err) => {
        console.log(err)
        alert('Erro desconhecido, contacte o administrador do sistema.')
      })
    }
  },
  created() {
    let teste = {
      user: "Pedro",
      nivelAcesso: "1"
    }
    localStorage.setItem('usuario', JSON.stringify(teste))
  }
}
</script>

<style>
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
