<template>
    <div class="card">
      <div class="flex">
        <div class="flex justify-start items-center flex-wrap">
          <div class="title w-full">
            <h1 class="h1-style">Titulo: {{titulo}}</h1> <span v-if="status === 1 && nivel_acesso > 0" class="desativado"> Desativado</span>
            <span v-if="status === 2" class="emprestado"> Emprestado</span>
            <span v-if="status === 0" class="disponivel"> Disponivel</span>
          </div>
          <div class="w-full">
            <p>Total de Paginas: <b>{{paginas}}</b></p>
            <p>Idioma: <b>{{idioma}}</b></p>
            <p v-if="editora !== ''">Editora: <b>{{editora}}</b></p>
            <p>ISBN-10: <b>{{isbn10}}</b></p>
            <p>ISBN-13: <b>{{isbn13}}</b></p>
          </div>
        </div>
        <slot></slot>
    </div>
    </div>
  </template>

  <script>
import internal from 'stream';

  export default {
    name: "CardLivro",
    data() {
      return{
        nivel_acesso: JSON.parse(localStorage.getItem('usuario')).nivel_acesso
      }
    },
    props:{
      titulo: {
        required: true,
        type: String
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
        default: '',
        type: String
      },
      isbn10: {
        required: true,
        type: String
      },
      isbn13: {
        required: true,
        type: String
      },
      status:{
        required: true,
        type: Boolean
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
    .desativado{
      @apply bg-red-700 rounded-lg text-white p-1 ml-5
    }
    .disponivel{
      @apply bg-green-700 rounded-lg text-white p-1 ml-5
    }
    .emprestado{
      @apply bg-yellow-500 rounded-lg text-white p-1 ml-5
    }

  </style>
