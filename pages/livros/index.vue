<template>


    <section id="livro">
      <div class="md:pl-20 md:pr-20 mt-32">
        <div class="w-full flex justify-end mb-12">
            <nuxt-link to ="/livros/cadastrarLivro"><Button text-button="Cadastrar Livros"></Button></nuxt-link>
        </div>
        <div class="mb-6" v-for="{id_exemplar, nome_titulo, nome_editora, nome_idioma, paginas_titulo, isbn_10, isbn_13} in itens" :key="id_exemplar">
            <CardLivro :titulo="nome_titulo" :paginas="paginas_titulo" :idioma="nome_idioma" :editora="nome_editora" :isbn10="isbn_10" :isbn13="isbn_13">
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
  </style>
  