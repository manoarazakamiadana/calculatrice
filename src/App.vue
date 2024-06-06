<template>
  <h1 class="titre">CALCULATRICE</h1>
  <div class="calculatrice">
    <div class="ecran">
      <h1 v-if="calcul">{{ calcul }}</h1>
      <h1 v-else>0</h1>
    </div>
    <div class="button-container">
      <div class="nombre-container">
        <button @click="ajouterCalcul('(')" class="button_appart">(</button>
        <button @click="ajouterCalcul(')')" class="button_appart">)</button>
        <button @click="effacer" class="button_appart">Del</button>
        <button v-for="n in 10" :key="n" @click="ajouterCalcul(10-n)" class="nombre">{{ 10-n }}</button>
        <button @click="ajouterCalcul('00')" class="nombre">00</button>
        <button @click="ajouterCalcul('.')" class="nombre">.</button>
      </div>
      <div class="operation-container">
        <button @click="effacerTout" class="button_delete_all">C</button>
        <button v-for="operateur in operation" :key="operateur" @click="ajouterCalcul(operateur)">{{ operateur }}</button>
      </div>
      <button @click="calculer" id="calculer">=</button>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      calcul : '',
      operation : ['+', '-', 'x', '÷'],
    }
  },
  methods: {
    ajouterCalcul (n) {
      this.calcul += n.toString()
    },
    effacerTout () {
      this.calcul = ''
    },
    effacer () {
      this.calcul = this.calcul.slice(0, -1)
    },
    ajouterCalculKey (event) {
      console.log(event.key)
      if (event.key=='=' || event.key=='Enter') {
        this.calculer();
        event.preventDefault()
      } else if (event.key=='Backspace') {
        this.calcul = this.calcul.slice(0, -1)
        event.preventDefault()
      } else {
        let button = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '+', '-', '*', '/', ')', '(', '.']
        for (let i = 0; i < button.length; i++) {
          if (event.key == button[i]) {
            this.calcul += button[i]
            event.preventDefault()
          }
        }
      }
    },
    calculer () {
      this.calcul = eval(this.calcul.replace('x', '*').replace('÷', '/'));
    }
  },
  mounted() {
    document.addEventListener('keydown', this.ajouterCalculKey);
  },
}
</script>

<style>

</style>