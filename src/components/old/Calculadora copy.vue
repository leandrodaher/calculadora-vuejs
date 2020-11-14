<template>
  <div class="calc">
    <!-- <h1 class="float">{{ title }}</h1> -->
    <div class="painel">
      <h1>Painel</h1>
    </div>
    <div class="content-buttons">
      <div class="button">%</div>
      <div class="button">CE</div>
      <div class="button">C</div>
      <div class="button">&larr;</div>
      
      <div class="button">x^2</div>
      <div class="button">x^y</div>
      <div class="button">sqrt(x)</div>
      <div class="button">/</div>

      <div class="button">7</div>
      <div class="button">8</div>
      <div class="button">9</div>
      <div class="button">/</div>

      <div class="button">4</div>
      <div class="button">5</div>
      <div class="button">6</div>
      <div class="button">*</div>

      <div class="button">1</div>
      <div class="button">2</div>
      <div class="button">3</div>
      <div class="button">-</div>

      <div class="button"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculadora",
  props: {
    title: String,
  },

  data() {
    //
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
*, *::after, *::before {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}


h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.calc {
  position: relative;

  width: 350px;
  height: 750px;
  
  border: 1px solid black;

  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  
  flex-grow: 0;
  flex-shrink: 0;
}

.float {
  position: absolute;
  transform: translateY(-100%);
}

.painel {
  width: 100%;
  height: 64px;

  /* border: 1px solid yellow; */
  background: #aaa;

  flex-shrink: 0;
}


.content-buttons {
  width: 100%;

  /* border: 1px solid green; */

  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: flex-start;
  align-content: flex-start; /* mantem os flex itens sem margem após quebra de linha */
  flex-wrap: wrap;
  flex-grow: 1;
  flex-shrink: 0;

}

.button {
  width: 25%;
  height: 16.7%;

  font-size: 16px;

  /* border: 1px solid red; */
  background: #ccc;

  display: flex;
  flex-shrink: 0;

  justify-content: center;
  align-items: center;

}

</style>
