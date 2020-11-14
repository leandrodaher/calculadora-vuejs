<template>
  <div class="calc">
    <!-- <h1 class="float">{{ title }}</h1> -->
    <div class="painel-content noselect">
      <Painel>
        <h1>{{ formatValue }}</h1>
      </Painel>
    </div>

    <div class="content-buttons grid">
      <Button @click="insert('%')" v-bind:high="true" class="grid-item">%</Button>
      <Button @click="insert('')" v-bind:high="true" class="grid-item">CE</Button>
      <Button @click="insert('')" v-bind:high="true" class="grid-item">C</Button>
      <Button @click="backspace()" v-bind:high="true" class="grid-item">&larr;</Button>
      
      <Button @click="insert('^2')" v-bind:high="true" class="grid-item">x^2</Button>
      <Button @click="insert('^')" v-bind:high="true" class="grid-item">x^y</Button>
      <Button @click="insert('C')" v-bind:high="true" class="grid-item">sqrt(x)</Button>
      <Button @click="insertOp('/')" v-bind:high="true" class="grid-item">/</Button>

      <Button @click="insert('7')" class="grid-item">7</Button>
      <Button @click="insert('8')" class="grid-item">8</Button>
      <Button @click="insert('9')" class="grid-item">9</Button>
      <Button @click="insertOp('*')" v-bind:high="true" class="grid-item">*</Button>

      <Button @click="insert('4')" class="grid-item">4</Button>
      <Button @click="insert('5')" class="grid-item">5</Button>
      <Button @click="insert('6')" class="grid-item">6</Button>
      <Button @click="insertOp('-')" v-bind:high="true" class="grid-item">-</Button>

      <Button @click="insert('1')" class="grid-item">1</Button>
      <Button @click="insert('2')" class="grid-item">2</Button>
      <Button @click="insert('3')" class="grid-item">3</Button>
      <Button @click="insertOp('+')" v-bind:high="true" class="grid-item">+</Button>

      <Button @click="insert('C')" class="grid-item">+/-</Button>
      <Button @click="insert('0')" class="grid-item">0</Button>
      <Button @click="insertDot()" v-bind:inactive="dotState" class="grid-item">,</Button>
      <Button @click="insertEqual()" v-bind:inactive="calcState == 0 ? true : false" v-bind:high="true" class="grid-item">=</Button>
    </div>
  </div>
</template>

<script>
import Button from './Button';
import Painel from './Painel';

export default {
  name: "Calculadora",
  components: {
    Button,
    Painel,
  },
  props: {
    title: String
  },

  data() {
    return {
      value: '',
      calcState: 0,
      dotState: false,

      num1: null,
      num2: null,
      op: '',
    }
  },

  methods: {
    insert(n) {
      if (this.value.length <= 0 && n == '0') {
        return 0;
      }

      // se houver virgula, permitir 1 caractere a mais, pois virgula não conta como caractere numérico
      // os caracteres de ponto não fazem parte do IF pois são visiveis apenas na camada de visualização, não estão presentes em this.value
      if ( (!this.dotState && this.value.length < 16) || (this.dotState && this.value.length < 17) ) {
        this.value += n;
      }
      
      // console.log( n, this.value, this.dotState, this.value[this.value.length-1] );
    },

    insertOp(n) {
      this.op = n;
      this.dotState = false;
      this.num1 = parseFloat(this.value);
      this.value = '';
      this.calcState = 1;
    },

    insertDot() {
      if (!this.dotState) {
        let n = ',';
        if (this.value.length < 1)
          n = '0,'

        this.dotState = true;
        this.insert(n);
      }
    },

    insertEqual() {
      if (this.calcState == 0) {
        return 0;
      } else {
        this.insert('=');
      }
    },

    backspace() {
      this.value = this.value.slice(0, length-1);
      if (this.value.search(',') == -1) {
        this.dotState = false;
      }
    },

    formatNumber(val) {
      /* https://stackoverflow.com/questions/2254185/regular-expression-for-formatting-numbers-in-javascript */
      // this.value.replace(/(\d)(?=(\d{3})+(?!\d))/g, "$1.");

      let s, n1, n2;
      // separa array numeros antes e depois da virgula
      s = val.split(',');

      // formata numeros antes da vírgula
      n1 = s[0].replace(/(\d)(?=(\d{3})+(?!\d))/g, "$1.");

      // numeros depois da virgula
      n2 = s[1] ? (',' + s[1]) : ''; //s[1] || '';

      // junta numeros formatados mais casas após a vírgula
      return n1 + n2;
    },

  },

  computed: {
    formatValue() {
      let r = !this.value ? '0' : this.formatNumber(this.value);

      return r;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
*, *::after, *::before {
  margin: 0;
  padding: 0;
  box-sizing: border-box;

  font-family: monospace;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(24%, 1fr));
  grid-template-rows: 1fr;
  grid-gap: 1px;
}

.grid-item {
  display: flex;
  justify-content: center;
  align-items: center;
}

.grid-item:before {
  content: "";
  display: block;
  height: 0;
  width: 0;
  /* padding-bottom: calc(9/16 * 100%); */
  padding-bottom: calc(1/1 * 100%);
}


.calc {
  position: relative;

  width: 350px;
  /* height: 750px; */
  height: auto;
  
  /* border: 1px solid black; */
  background-color: rgb(42, 42, 54);

  -webkit-box-shadow: 0px 0px 16px 0px rgba(0,0,0,0.75);
  -moz-box-shadow: 0px 0px 16px 0px rgba(0,0,0,0.75);
  box-shadow: 0px 0px 16px 0px rgba(0,0,0,0.75);
}

.float {
  position: absolute;
  transform: translateY(-100%);
}

.painel-content {
  display: block;
  width: 100%;
  height: 75px;
  /* border: 1px solid yellow; */
}

.content-buttons {
  width: 100%;
}
</style>
