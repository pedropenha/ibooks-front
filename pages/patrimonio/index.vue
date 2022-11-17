<template>
  <section id="patrimonio">
    <div class="md:pl-20 md:pr-20 mt-32">
      <div class="w-full flex justify-end mb-12">
        <nuxt-link to="/patrimonio/cadastraPatrimonio"><button class="primary">Cadastrar patrimonio</button></nuxt-link>
      </div>
      <div class="mb-6" v-for="{idPatrimonio, nome_patrimonio, numero_patrimonio, valor_patrimonio} in itens" :key="idPatrimonio">
        <Card :patrimonio-number="numero_patrimonio" :valor-compra="valor_patrimonio" quantidade="1" :titulo="nome_patrimonio">
          <div class="action">
            <button class="info mr-6">Editar</button>
            <button @click.prevent="excluir(idPatrimonio)" class="danger">Excluir</button>
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
  methods:{
    excluir(id){
      if(confirm("Deseja realmente excluir?")){
        this.$axios.post('/patrimonio/delete', {idPatrimonio: id})
        location.reload()
      }
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
.primary{
  @apply bg-green-400 shadow-md shadow-green-300 text-white rounded-md transition p-4;
}
.primary:hover{
  @apply bg-green-500 shadow-green-400;
}
.danger{
  @apply bg-red-600 shadow-md shadow-red-500 text-white rounded-md transition p-4;
}
.danger:hover{
  @apply bg-red-700 shadow-red-600;
}
.info{
  @apply bg-blue-600 shadow-md shadow-blue-500 text-white rounded-md transition p-4;
}
.info:hover{
  @apply bg-blue-700 shadow-blue-600;
}
</style>
