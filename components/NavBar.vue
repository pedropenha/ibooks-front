<template>
  <div class="w-screen shadow-lg p-1 flex justify-between">

    <div class="w-32 h-auto flex items-center">
      <img class="w-full" src="~/assets/images/Logo.svg" alt="Logo"/>
    </div>

    <div class="flex items-center">
      <nuxt-link to="/patrimonio" :class='this.$route.path.includes("/patrimonio")  ? "ativo" : "rota"'>Patrimonio</nuxt-link>
      <nuxt-link to="/livros" :class='this.$route.path === "/livros" ? "ativo ml-2" : "rota ml-2"'>Livros</nuxt-link>
    </div>

    <div class="flex items-center">
      <nuxt-link to="/login" class="flex justify-end" v-if="!logado"><button class="primary">Logar</button></nuxt-link>
      <button class="danger flex justify-end" v-if="logado" @click="sair">Sair</button>
    </div>

  </div>
</template>

<script>
export default {
  data(){
    return{
      logado: localStorage.getItem('usuario') !== null,
      nivel_acesso: JSON.parse(localStorage.getItem('usuario'))
    }
  },
  methods:{
    sair(){
      localStorage.clear()
      window.location.href = '/login'
    }
  }
}
</script>

<style>
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
.ativo{
  @apply text-blue-700 font-bold text-xl;
}
.rota{
  @apply font-bold transition text-xl;
}
.rota:hover{
  @apply text-blue-700 font-bold;
}
</style>
