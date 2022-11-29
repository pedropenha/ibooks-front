<template>
  <section id="livro">
    <NavBar/>
    <div class="md:pl-20 md:pr-20 mt-32">
      <div class="w-full flex justify-end mb-12">
        <nuxt-link to="/livros/cadastrarLivro">
          <button class="primary" v-if="nivel_acesso === 1">Cadastrar livro</button>
        </nuxt-link>
      </div>
      <div class="mb-6"
           v-for="{id_exemplar, nome_titulo, nome_editora, nome_idioma, paginas_exemplar, isbn_10, isbn_13, status, exemplares_disponiveis, id_pessoa_fisica} in itens"
           :key="id_exemplar">
        <CardLivro :titulo="nome_titulo" :paginas="paginas_exemplar" :idioma="nome_idioma" :editora="nome_editora"
                   :isbn10="isbn_10" :isbn13="isbn_13" :status="status">
          <div class="action">
            <nuxt-link :to="'/livros/emprestarExemplar/'+id_exemplar" v-if="nivel_acesso === 1 && status === 0">
              <button class="success mr-6">Emprestar</button>
            </nuxt-link>

            <nuxt-link :to="'/livros/baixaDeLivro/'+id_exemplar" v-if="status === 0 && nivel_acesso === 1">
              <button class="warning mr-6">Dar baixa no livro</button>
            </nuxt-link>

            <nuxt-link :to="'/livros/'+id_exemplar" v-if="nivel_acesso === 1">
              <button class="info mr-6">Editar</button>
            </nuxt-link>
            <button @click.prevent="excluir(id_exemplar)" class="danger" v-if="nivel_acesso === 1">Excluir</button>
            <button  v-if="nivel_acesso === 0" @click.prevent="fila_espera(id_exemplar)" class="info mr-6" :disabled="flag === id_exemplar">
              Entrar na fila de espera
            </button>
          </div>
        </CardLivro>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Livro',
  data() {
    return {
      flag: false,
      itens: '',
      pessoa: JSON.parse(localStorage.getItem('usuario')).id_pessoa_fisica,
      nivel_acesso: JSON.parse(localStorage.getItem('usuario')).nivel_acesso,
    }
  },
  methods: {
    fila_espera(id_exemplar) {
      if (confirm("Deseja realmente entrar na fila de espera?")) {
        this.$axios.post('/filaDeEspera/',{
          id_exemplar: id_exemplar,
          id_pessoa_fisica: this.pessoa

        }).then((response) => {
          this.flag = id_exemplar;
          // location.reload()
        }).catch((erro) => {
          alert(erro)
        })
      }
    },
    excluir(id) {
      if (confirm("Deseja realmente excluir?")) {
        this.$axios.delete('/livro/'+id).then((response) => {
          location.reload()
          }).catch((erro) => {
          alert(erro)
        })
      }
    },

  },

  created() {
    if(localStorage.getItem('usuario') !== null && JSON.parse(localStorage.getItem('usuario')).nivel_acesso >0){
      this.$axios.get('livro/').then((response) => {

        this.itens = response.data.mensagem;
        console.log(response.data.mensagem);
      }).catch((e) => {
        console.log(e);
      })
    }
    else{
      this.$axios.get('livro/grupo').then((response) => {
        this.itens = response.data.mensagem;
      }).catch((e) => {
        console.log(e);
      })
    }



    if(localStorage.getItem('usuario') === null) {
      window.location.href = "/login"
    }
  },
}
</script>

<style scoped>
.primary {
  @apply bg-green-400 shadow-md shadow-green-300 text-white rounded-md transition p-4;
}

.primary:hover {
  @apply bg-green-500 shadow-green-400;
}

.danger {
  @apply bg-red-600 shadow-md shadow-red-500 text-white rounded-md transition p-4;
}

.danger:hover {
  @apply bg-red-700 shadow-red-600;
}

.info {
  @apply bg-blue-600 shadow-md shadow-blue-500 text-white rounded-md transition p-4;
}

.info:hover {
  @apply bg-blue-700 shadow-blue-600;
}

.info:disabled {
  @apply opacity-30 cursor-not-allowed;
}

.warning {
  @apply bg-yellow-400 shadow-yellow-300 shadow-md text-white rounded-md transition p-4;
}

.warning:hover {
  @apply bg-yellow-500 shadow-yellow-500;
}

.success{
  @apply bg-green-600 shadow-green-400 shadow-md text-white rounded-md transition p-4
}

.success:hover{
  @apply bg-green-700 shadow-green-700;
}

</style>

