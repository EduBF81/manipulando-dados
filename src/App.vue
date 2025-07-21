<template>
  <h3>Métodos</h3>
  <p>{{ total }}</p>
  <button @click="calcula('-')">-</button>
  <button @click="calcula('+')">+</button>
  
  <p>Nome do Computador: {{ nomeFormatado }}</p>
  <label>Input a computar </label>
  <input type="text" v-model="nome" />
</template>

<script>


export default {
  name: 'lv-contador',
  data() {
    return {
      total: 10,
      nome: 'Eduardo',
    }
  },
  // Métodos são funções que podem ser chamadas
  // a partir do template ou de outros métodos.
  // Eles são usados para manipular dados, realizar cálculos
  // ou executar ações quando um evento ocorre.
  // Métodos são reativos, ou seja, quando uma propriedade
  // reativa é alterada, o método é chamado novamente.
  // Eles são úteis para manipular dados, realizar cálculos
  // ou executar ações quando um evento ocorre.
  // Métodos são reativos, ou seja, quando uma propriedade
  // reativa é alterada, o método é chamado novamente.
  methods: {
    calcula(sinal) {
      this.total = (sinal == '-') ? this.total - 1 : this.total + 1;
    },
  },
  // Computed properties são propriedades que são computadas
  // a partir de outras propriedades reativas.
  // Elas são úteis para transformar dados ou realizar cálculos
  // baseados em dados reativos, e são recalculadas apenas quando
  // as dependências reativas mudam.
  // Computed properties são mais eficientes do que métodos
  // porque são armazenadas em cache e só são recalculadas
  // quando suas dependências mudam.
  // Elas são usadas para transformar dados ou realizar cálculos
  // baseados em dados reativos, e são recalculadas apenas quando
  // as dependências reativas mudam.
  computed: {
    nomeFormatado() {
      console.log('Chamando Computed');
      return this.nome.toUpperCase();
    }
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
