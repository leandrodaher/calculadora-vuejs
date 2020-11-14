<template>
    <div @click="$emit('click')" class="button noselect" v-bind:class="{ active: inactive, highlight: high }">
        <slot></slot>
    </div>
</template>

<script>
export default {
    name: "Button",
    props: {
        high: Boolean,
        inactive: Boolean,
    },
}
</script>

<style scoped>
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