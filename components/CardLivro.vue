<template>
    <div class="card">
      <div class="flex">
        <div class="flex justify-start items-center flex-wrap">
          <div class="title w-full">
            <h1 class="h1-style">Titulo: {{titulo}} - Quantidade de exemplares: {{total}}</h1>
          </div>
          <div class="w-full">
            <p>Total de Paginas: <b>{{paginas}}</b></p>
            <p>Idioma: <b>{{idioma}}</b></p>
            <p>Editora: <b>{{editora}}</b></p>
            <p>ISBN-10: <b>{{isbn10}}</b></p>
            <p>ISBN-13: <b>{{isbn13}}</b></p>
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
import internal from 'stream';

  export default {
    name: "CardLivro",
    props:{
      titulo: {
        required: true,
        type: String
      },
      total: {
        required: true,
        type: Number
      },
      paginas: {
        required: true,
        type: Number
      },
      idioma: {
        required: true,
        type: String
      },
      editora: {
        required: true,
        type: String
      },
      isbn10: {
        required: true,
        type: String
      },
      isbn13: {
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
  