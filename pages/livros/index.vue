<template>
    <section id="livro">
      <div class="md:pl-20 md:pr-20 mt-32">
        <div class="w-full flex justify-end mb-12">
            <nuxt-link to ="/livros/cadastrarLivro"><button class="primary">Cadastrar livro</button></nuxt-link>
        </div>
        <div class="mb-6" v-for="{id_exemplar, nome_titulo, nome_editora, nome_idioma, paginas_titulo, isbn_10, isbn_13} in itens" :key="id_exemplar">
          <CardLivro :titulo="nome_titulo" :paginas="paginas_titulo" :idioma="nome_idioma" :editora="nome_editora" :isbn10="isbn_10" :isbn13="isbn_13">
            <div class="action">
              <nuxt-link :to="'/livros/'+id_exemplar"><button class="info mr-6">Editar</button></nuxt-link>
              <button @click.prevent="excluir(id_exemplar, nome_titulo)" class="danger">Excluir</button>
            </div>
          </CardLivro>
        </div>
      </div>
    </section>
  </template>

  <script>
  export default {
  name: 'Livro',
  data(){
    return{
      itens: '',
    }
  },
    methods:{
      excluir(id)
      {
        if(confirm("Deseja realmente excluir?")){
          this.$axios.post('/livro/deletar', {id_exemplar: id})
          location.reload()
        }
      }
    },
  created() {
    this.$axios.get('livro/').then((response) => {

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
