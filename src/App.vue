<template>
  <h1>Capitulo 5 - Manipulando dados</h1>
  <h1>5.1 Methods - Bloco de ações</h1>
  <h3>Métodos</h3>
  <p>{{ total }}</p>
  <button @click="calcula('-')">-</button>
  <button @click="calcula('+')">+</button>
  <p>Utiliza metódos para modificar a variavel total</p>

  <h1>5.2 Computed properties - Modificando dados para exibilos</h1>
  <p>Nome do Computador: {{ nomeFormatado }}</p>
  <label>Input a computar </label>
  <input type="text" v-model="nomeFormatado" />
  <p>Retorna somente as 3 primeiras letras do nome digitado usando setters</p>

  <h1>5.3 Watchers - Dados que podem esperar</h1>
  <label for="">Input a observar</label>
  <input type="text" v-model="busca" />
  <p v-text="resultado"></p>
  <p>Utiliza watchers para observar mudanças na propriedade busca</p>
  <p>Quando a propriedade busca é alterada, o watcher é acionado e chama o método recolheResposta</p>
  <p>O método recolheResposta simula uma espera de 500ms e depois atualiza a propriedade resultado</p>
  <p>O watcher é útil para realizar ações assíncronas, como chamadas de API, ou para executar ações quando uma
    propriedade reativa muda</p>

  <h1>5.4 Teste seu avanço</h1>
  <h3>Memorize a teoria</h3>
  <p>concatenar o nome e sobrenome</p>
  <NomeCompleto />
  <p>valor formatado usando computed recomendado</p>
  <label for="">valor formatado em R$</label>
  <input type="number" v-model.number="valor" />
  <p>O valor formatado é uma propriedade computada que formata o valor em reais (R$)</p>
  <p>O valor formatado é atualizado automaticamente quando o valor é alterado</p>
  <p>O valor formatado é usado para exibir</p>
  <p>{{ valorFormatado }}</p>

  <h3>Monitorando a hora com watchers</h3>
  <p>Hora atual: {{ horaAtualFormatada }}</p>
  <p v-if="mensagem">{{ mensagem }}</p>
  <h3>Alerta ao passar o mouse em uma tag</h3>
  <span @mouseover="mostrarAlerta">Passe o mouse aqui</span>

  <h1>Na Prática</h1>
  <input type="text" v-model="name" />
  <p>Nome digitado: {{ name }}</p>
  <small>{{ status }}</small>
  <button @click="status = 'Olá ' + name">clique para saudar</button>
  <label for="">observado o innput</label>
  <input type="text" v-model="mudarStatus" />
  <p v-text="status"></p>

</template>

<script>
import NomeCompleto from './components/NomeCompleto.vue';

export default {
  name: 'lv-contador',
  components: {
    NomeCompleto
  },
  data() {
    return {
      // data é um objeto que contém as propriedades reativas
      // que serão usadas no template.
      // Propriedades reativas são aquelas que, quando alteradas,
      // fazem com que o template seja re-renderizado.
      // Elas são declaradas dentro do objeto data e podem ser
      // acessadas diretamente no template usando a sintaxe {{ propriedade }}.
      total: 10,
      nome: 'Eduardo',
      name:'',
      resultado: '',
      busca: '',
      valor: 0.0, // Exemplo de valor que será formatado
      horaAtual: new Date(),
      mensagem: '',
      status: 'Digite seu nome acima...',
    }
  }, watch: {
    // Watchers são usados para observar mudanças em propriedades reativas
    // e executar ações quando essas mudanças ocorrem.
    // Eles são úteis para realizar ações assíncronas, como chamadas de API,
    // ou para executar ações quando uma propriedade reativa muda.
    busca: function () {
      this.resultado = 'Aguardando o término da digitação...';
      this.recolheResposta();
    },
    horaAtual(novaHora) {
      const minutos = novaHora.getMinutes();
      if (minutos === 0 || minutos === 30) {
        // acionarAlerta();
      }
    },

    mudarStatus: function () {
      // Este watcher é acionado quando a propriedade name muda
      // e pode ser usado para executar ações quando o nome muda.
      this.status = 'Recebendo' ;
      this.recolheResposta();
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
    recolheResposta() {
      // Este método é um exemplo de como você pode
      // manipular dados ou realizar ações quando um evento ocorre.
      // Ele pode ser chamado a partir do template usando a sintaxe @click="recolheResposta".
      let valor = this.busca
      setTimeout(() => {
        this.resultado = `Terminou de digitar...` + valor;
      }, 2000);
    }
  },
  atualizarHora() {
    // Este método é usado para atualizar a hora atual
    // e pode ser chamado a partir do template usando a sintaxe @click="atualizarHora".
    this.horaAtual = new Date();
  },
  acionarAlerta() {
    this.mensagem = `⏱️ O relógio marcou! Ação disparada!`;
    // Se quiser limpar a mensagem após alguns segundos:
    setTimeout(() => {
      this.mensagem = '';
    }, 4000);
  },
  mostrarAlerta() {
    alert('Você passou o mouse sobre a tag!');
  },
  mounted() {
    // O método mounted é chamado quando o componente é montado
    // e é um bom lugar para inicializar dados ou realizar ações
    // que precisam ser executadas quando o componente é exibido.
    // Aqui, estamos configurando um intervalo para atualizar a hora atual
    // a cada segundo.
    setInterval(() => {
      this.horaAtual = new Date();
    }, 1000);
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
    nomeFormatado: {
      // console.log('Chamando Computed');
      // return this.nome.toUpperCase();
      get() {
        return this.nome.toUpperCase();
      },
      set(novoNome) {
        this.nome = novoNome.substring(0, 3);
      }
    },
    valorFormatado() {
      return this.valor.toLocaleString('pt-BR', {
        style: 'currency',
        currency: 'BRL'
      });

    },
    horaAtualFormatada() {
      // Este watcher é acionado quando a hora atual formatada muda
      // e pode ser usado para executar ações quando a hora muda.
      return this.horaAtual.toLocaleTimeString('pt-BR', {
        hour: '2-digit',
        minute: '2-digit',
        second: '2-digit'
      });
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
