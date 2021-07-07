<template>
<div>
  <h2>Sobre</h2>
  <p v-if="autor">Autor: {{ autor }}</p>
  <input type="text" v-model="autor">
</div>
</template>

<script>
export default {
  data() {
    return {
      autor: ''
    }
  },
  created(){
    console.log("Created")
  },
  destroyed () {
    console.log("Destroyes")
  },
  activated() {
    console.log("Activado")
  },
  deactivated() {
    console.log("Desativado")
  }
}
</script>