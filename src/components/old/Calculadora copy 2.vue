<template>
  <div class="calc">
    <!-- <h1 class="float">{{ title }}</h1> -->
    <div class="painel noselect">
      <h1>{{ formatValue }}</h1>
    </div>

    <div class="content-buttons grid">
      <div @click="insert('%')" class="button grid-item noselect highlight">%</div>
      <div @click="insert('')" class="button grid-item noselect highlight">CE</div>
      <div @click="insert('')" class="button grid-item noselect highlight">C</div>
      <div @click="backspace()" class="button grid-item noselect highlight">&larr;</div>
      
      <div @click="insert('^2')" class="button grid-item noselect highlight">x^2</div>
      <div @click="insert('^')" class="button grid-item noselect highlight">x^y</div>
      <div @click="insert('C')" class="button grid-item noselect highlight">sqrt(x)</div>
      <div @click="insertOp('/')" class="button grid-item noselect highlight">/</div>

      <div @click="insert('7')" class="button grid-item noselect">7</div>
      <div @click="insert('8')" class="button grid-item noselect">8</div>
      <div @click="insert('9')" class="button grid-item noselect">9</div>
      <div @click="insertOp('*')" class="button grid-item noselect highlight">*</div>

      <div @click="insert('4')" class="button grid-item noselect">4</div>
      <div @click="insert('5')" class="button grid-item noselect">5</div>
      <div @click="insert('6')" class="button grid-item noselect">6</div>
      <div @click="insertOp('-')" class="button grid-item noselect highlight">-</div>

      <div @click="insert('1')" class="button grid-item noselect">1</div>
      <div @click="insert('2')" class="button grid-item noselect">2</div>
      <div @click="insert('3')" class="button grid-item noselect">3</div>
      <div @click="insertOp('+')" class="button grid-item noselect highlight">+</div>

      <div @click="insert('C')" class="button grid-item noselect">+/-</div>
      <div @click="insert('0')" class="button grid-item noselect">0</div>
      <div @click="insertDot()" v-bind:class="{ active: dot }" class="button grid-item noselect">,</div>
      <div @click="insert('C')" class="button grid-item noselect highlight">=</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculadora",
  props: {
    title: String
  },

  data() {
    return {
      value: '',
      dot: false,
    }
  },

  methods: {
    insert(n) {
      this.value += n;
      
      // console.log( n, this.value, this.dot, this.value[this.value.length-1] );
    },

    insertOp(n) {
      this.insert(n);
      this.dot = false;
    },

    insertDot() {
      if (!this.dot) {
        let n = ',';
        if (this.value.length < 1)
          n = '0,'

        this.dot = true;
        this.insert(n);
      }
    },

    backspace() {
      this.value = this.value.slice(0, length-1);
      if (this.value.search(',') == -1) {
        this.dot = false;
      }
    },
  },

  computed: {
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

    formatValue() {
      return this.value;
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

.painel {
  width: 100%;
  height: 75px;
  /* border: 1px solid yellow; */
  
  background-color: rgb(42, 42, 54);

  padding: 14px;

  display: flex;
  justify-content: flex-end;
  align-items: center;

  color: #fff;
}

.content-buttons {
  width: 100%;
}

.button {
  font-size: 16px;
  color: rgba(255, 255, 255, 0.6);

  /* border: 1px solid red; */
  
  background-color: rgb(18, 18, 31);

  display: flex;
  justify-content: center;
  align-items: center;

  transition: all 0.2s;
}

.button:hover {
  background-color: rgb(54, 54, 75);
  color: #fff;
}

/* evita seleção do texto */
  /* https://stackoverflow.com/questions/826782/how-to-disable-text-selection-highlighting */
.noselect {
  -webkit-touch-callout: none; /* iOS Safari */
    -webkit-user-select: none; /* Safari */
     -khtml-user-select: none; /* Konqueror HTML */
       -moz-user-select: none; /* Old versions of Firefox */
        -ms-user-select: none; /* Internet Explorer/Edge */
            user-select: none; /* Non-prefixed version, currently
                                  supported by Chrome, Edge, Opera and Firefox */
}

.highlight {
  background-color: rgb(50, 50, 100);
  color: rgba(255, 255, 255, 0.6);
}

.highlight:hover {
  background-color: rgb(83, 83, 148);
  color: #fff;
}

.active {
  /* visibility: hidden; */
  background-color: rgba(18, 18, 31, 0.2);
}

.active:hover {
  /* visibility: hidden; */
  background-color: rgba(18, 18, 31, 0.2);
}

</style>
