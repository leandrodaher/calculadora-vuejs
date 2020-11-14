<template>
    <div class="painel noselect">
        <slot></slot>
    </div>
</template>

<script>
export default {
    name: "Painel",
    
}
</script>

<style scoped>
.painel {
  width: 100%;
  height: 100%;
  /* border: 1px solid yellow; */
  
  background-color: rgb(42, 42, 54);

  padding: 14px;

  display: flex;
  justify-content: flex-end;
  align-items: center;

  flex-shrink: 0;
  flex-grow: 0;
  
  font-family: 'Overpass Mono', monospace;
  font-size: 14px;
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
</style>