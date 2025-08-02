<template>
  <div>
    <p>Nome completo: {{ nomeCompleto }}</p>
  </div>
</template>

<script>
export default {
    name: 'NomeCompleto',
  // O componente NomeCompleto exibe o nome completo
  data() {
    return {
      nome: 'Eduardo',
      sobrenome: 'Borges'
    }
  },
  computed: {
    nomeCompleto() {
      return `${this.nome} ${this.sobrenome}`;
    }
  }
}
</script>
