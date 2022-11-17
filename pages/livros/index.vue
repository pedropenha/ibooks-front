<template>
    <section id="livros">
      <div class="md:pl-20 md:pr-20 mt-32">
        <div class="w-full flex justify-end mb-12">
          <Button text-button="Cadastrar Livros"></Button>
        </div>
        <CardLivro titulo="Berserk" total="10" paginas="216" idioma="pt" editora="panini" isbn10="1010101010" isbn13="1313131313-133"></CardLivro>
      </div>
    </section>
  </template>
  
  <script>
  export default {
    name: 'Livros'
  }
  </script>
  
  <style scoped>
  </style>
  