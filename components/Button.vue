<template>
  <button :class="classButton">
    <div class="p-3">
      {{textButton}}
    </div>
  </button>
</template>

<script>
export default {
  name: 'Button',
  props:{
    textButton: {
      default: '',
      type: String
    },
    classButton: {
      default: 'primary',
      type: String
    }
  }

}
</script>

<style scoped>
  .primary{
    @apply bg-green-400 shadow-md shadow-green-300 text-white rounded-md transition;
  }
  .primary:hover{
    @apply bg-green-500 shadow-green-400;
  }
  .danger{
    @apply bg-red-600 shadow-md shadow-red-500 text-white rounded-md transition;
  }
  .danger:hover{
    @apply bg-red-700 shadow-red-600;
  }
  .info{
    @apply bg-blue-600 shadow-md shadow-blue-500 text-white rounded-md transition;
  }
  .info:hover{
    @apply bg-blue-700 shadow-blue-600;
  }
</style>
