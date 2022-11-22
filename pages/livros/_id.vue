<template>
  <section id="editarLivro">
    <div class="md:pl-20 md:pr-20 mt-32">
      <nuxt-link to="/livros" class="mb-36">
        <Button text-button="Voltar" class-button="info"></Button>
      </nuxt-link>
      <div class="div-form__control">
        <form class="form-control">

          <label for="titulo" class="label-control label-obrigatorio">Titulo *</label>
          <select class="input-form" v-model="titulo">
            <option v-for="{id_titulo, nome_titulo} in titulos" :key="id_titulo" :value="id_titulo" :selected="id_titulo === titulo">
              {{ nome_titulo }}
            </option>
          </select>

          <label for="paginas" class="label-control label-obrigatorio">Numero de Paginas *</label>
          <input class="input-form" id="paginas" v-model="paginas">

          <label for="idioma" class="label-control">Idioma *</label>
          <select class="input-form" v-model="idioma">
            <option v-for="{id_idioma, nome_idioma} in idiomas" :key="id_idioma" :value="id_idioma" :selected="id_idioma === idioma">{{ nome_idioma }}
            </option>
          </select>

          <label for="editora" class="label-control label-obrigatorio">Editora *</label>
          <select class="input-form" v-model="editora">
            <option v-for="{id_editora, nome_editora} in editoras" :key="id_editora" :value="id_editora" :selected="id_editora === editora">
              {{ nome_editora }}
            </option>
          </select>

          <label for="isbn10" class="label-control label-obrigatorio">Isbn_10 *</label>
          <input type="text" class="input-form" id="isbn10" v-model="isbn10" max="10">

          <label for="isbn13" class="label-control label-obrigatorio">Isbn_13 *</label>
          <input type="text" class="input-form" id="isbn13" v-model="isbn13" max="14">

          <button @click.prevent="enviar_dados" class="primary">Alterar Livro</button>
        </form>

      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      titulo: '',
      titulos: [],
      paginas: '',
      idiomas: [],
      idioma: '',
      editoras: [],
      editora: '',
      isbn10: '',
      isbn13: '',
      exemplar: ''
    }
  },
  methods: {
    enviar_dados() {
      if (confirm("Deseja realmente alterar?")) {
        this.$axios.post('livro/editar', {
          id_exemplar: this.exemplar,
          id_titulo: this.titulo,
          paginas_exemplar: this.paginas,
          id_idioma: this.idioma,
          id_editora: this.editora,
          isbn_10: this.isbn10,
          isbn_13: this.isbn13
        }).then((response) => {
          //location.reload()
          window.location.href = '/livros'
        }).catch((erro) => {
          alert(erro)
        })
      }
    }
  },

  created() {
    this.$axios.get('livro/' + this.$route.params.id).then((response) => {
      console.log(response.data.mensagem)
      this.itens = response.data.mensagem;

      this.exemplar = response.data.mensagem.id_exemplar
      this.titulo = response.data.mensagem.id_titulo
      this.paginas = response.data.mensagem.paginas_exemplar
      this.idioma = response.data.mensagem.id_idioma
      this.editora = response.data.mensagem.id_editora
      this.isbn10 = response.data.mensagem.isbn_10
      this.isbn13 = response.data.mensagem.isbn_13

    }).catch((e) => {
      // alert('erro ao atualizar')
    })

    this.$axios.get('livro/idiomas').then((response) => {
      this.idiomas = response.data.mensagem;
      console.log(this.idioma);
    })
    this.$axios.get('livro/editoras').then((response) => {
      this.editoras = response.data.mensagem;
      console.log(this.editora);
    })
    this.$axios.get('livro/titulos').then((response) => {
      this.titulos = response.data.mensagem;
      console.log(this.titulo);
    })

    if(localStorage.getItem('usuario') === null)
    {
      window.location.href = "/login"
    }

    if(JSON.parse(localStorage.getItem('usuario')).nivelAcesso < 1){
      window.location.href = '/livros'
    }
  }
}
</script>

<style scoped>
.input-form {
  @apply border-gray-400 w-full border-b transition mb-6
}

.input-form:hover {
  @apply border-gray-800
}

.form-control {
  @apply flex justify-center items-center flex-wrap w-6/12
}

.div-form__control {
  @apply w-full flex justify-center
}

.label-control {
  @apply w-full mb-2
}

.primary {
  @apply bg-green-400 shadow-md shadow-green-300 text-white rounded-md transition p-6;
}

.primary:hover {
  @apply bg-green-500 shadow-green-400;
}

.label-obrigatorio {
  @apply text-red-900;
}
</style>
