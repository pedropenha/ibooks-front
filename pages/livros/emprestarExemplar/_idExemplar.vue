<template>
  <section>
    <NavBar/>
    <div class="w-screen h-screen overflow-hidden flex items-center justify-center bg-white bg-cover bg-center">
      <div class="h-[40%] w-[35%] bg-[#f8f8f8] rounded-md ">
        <span class="grid">
        <form @submit.prevent="emprestar()" class="justify-self-center pt-5">
          <div>Nome do exemplar (*)</div>
          <input id="nomeEx" v-model="exempName" placeholder=" Ex: gato de botas" type="text" disabled class="border-2 border-gray-300 rounded h-10 w-80">
          <div>RM do usuario (*)</div>
          <input id="serie" v-model="rmUser" placeholder=" Ex: 132313" type="text" class="border-2 border-gray-300 rounded h-10 w-80">
          <br/><br/>
          <button class="bg-[#58E3C2] text-white h-10 w-52 rounded justify-self-center">Emprestar exemplar</button>
          <br/><br/>
        </form>
      </span>
      </div>
    </div>

  </section>
</template>

<script>
export default {
  name: 'emprestarExemplar',
  data(){
    return{
      exempName: '',
      exem_id: '',
      rmUser: '',
      id_colaborador: localStorage.getItem('usuario') !== null ? JSON.parse(localStorage.getItem('usuario')).id_pessoa_fisica : ''
    }
  },
  methods: {
    emprestar(){
      this.$axios.post('/emprestimo/', {
        id_cliente: this.rmUser,
        id_colaborador: this.id_colaborador,
        id_exemplar: this.exem_id
      }).then((response) => {
        console.log(response.data)
        alert(response.data.mensagem)
        window.location.href = "/livros"
      }).catch((e) => {
        console.log(e)
        alert("Nao foi possivel emprestar o livro: "+ e.message)
      })
    }
  },
  created() {
    this.$axios.get('/livro/'+this.$route.params.idExemplar).then((response) => {
      console.log(response.data.mensagem)
      this.exempName = response.data.mensagem.nome_titulo
      this.exem_id = response.data.mensagem.id_exemplar
    }).catch((e) => {
      alert(e)
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
