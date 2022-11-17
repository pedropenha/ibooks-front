<template>
  <section id="patrimonio">
    <div class="md:pl-20 md:pr-20 mt-32">
      <div class="w-full flex justify-end mb-12">
        <nuxt-link to="/patrimonio/cadastraPatrimonio"><Button text-button="Cadastrar patrimonio"></Button></nuxt-link>
      </div>
      <div class="mb-6" v-for="{idPatrimonio, nome_patrimonio, numero_patrimonio, valor_patrimonio} in itens" :key="idPatrimonio">
        <Card :patrimonio-number="numero_patrimonio" :valor-compra="valor_patrimonio" quantidade="1" :titulo="nome_patrimonio">
          <div class="action">
            <Button text-button="Editar" class-button="info" class="mr-6"></Button>
            <Button text-button="Excluir" class-button="danger"></Button>
          </div>
        </Card>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Patrimonio',
  data(){
    return{
      itens: '',
    }
  },
  created() {
    this.$axios.get('patrimonio/').then((response) => {

      this.itens = response.data.mensagem;
    }).catch((e) => {
      console.log(error);
    })
  }
}
</script>

<style scoped>
</style>
