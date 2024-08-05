<template>
  <div>
    <h1>{{  message  }}</h1>
  </div>
</template>

<script>
export default {
  name: 'MiComponente',
  data() {
    return {
      message: 'Hola Mundo'
    }
  },
  components:{
    //Registro de componentes
  },
  methods: {
    //métodos
  },
  computed: {
    //propiedades computades
  },
  props: {
    //propiedades del componente
  },
  emits:[] // eventos personalizados
}
</script>

<style>
h1 {
  color: #42b983;
}
</style>