<template>
  <div class="card">
    <div class="flex">
      <div class="flex justify-start items-center flex-wrap">
        <div class="title w-full">
          <h1 class="h1-style">Patrimonio: {{titulo}} - Quantidade: {{Quantidade}}</h1>
        </div>
        <div class="w-full">
          <p>Valor de compra: R$ <b>{{valorCompra}}</b></p>
          <p>Numero de patrimonio: <b>{{patrimonioNumber}}</b></p>
        </div>
      </div>
        <div class="action">
          <Button text-button="Editar" class-button="info" class="mr-6"></Button>
          <Button text-button="Excluir" class-button="danger"></Button>
        </div>
    </div>

  </div>
</template>

<script>
export default {
  name: "Card",
  props:{
    titulo: {
      required: true,
      type: String
    },
    Quantidade: {
      required: true,
      type: String
    },
    valorCompra: {
      required: true,
      type: String
    },
    patrimonioNumber: {
      required: true,
      type: String
    }
  }
}
</script>

<style>
  .card{
    @apply shadow-lg rounded-md w-full h-auto p-12 transition cursor-pointer border-2
  }
  .card:hover{
    @apply bg-gray-50
  }
  .title{
    @apply flex justify-start items-start
  }
  .h1-style{
    @apply font-bold text-xl
  }
  .action{
    @apply flex justify-end items-center w-full
  }

</style>
