<template>
  <div
    class="p-3"
    style="max-width: 400px; margin: 50px auto; background: #234"
  >
    <!-- Calculator Result -->
    <div
      class="
        w-full
        rounded
        m-1
        p-3
        text-center
        lead
        font-weight-bolt
        text-white
        bg-vue-dark
      "
    >
      {{ calculatorValue || 0 }}
    </div>

    <!-- Calculator Buttons -->
    <div class="row g-0">
      <div class="col-3" v-for="element in calculatorElements" :key="element">
        <div
          class="
            lead
            text-white 
            text-center
            m-1
            py-3
            bg-vue-dark
            rounded
            hover-class
          "
          @click="action(element)"
          :class="{'bg-vue-green': ['C','*','/','-','+','%','='].includes(element)}"
        >
          {{ element }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  props: {
    msg: String,
  },

  data() {
    return {
      calculatorValue: "",
      calculatorElements: [
        "C",
        "*",
        "/",
        "-",
        7,
        8,
        9,
        "+",
        4,
        5,
        6,
        "%",
        1,
        2,
        3,
        "=",
        0,
        ".",
      ],
      operator: null,
      previousCalculatorValue: '',
    };
  },

  methods: {
    action(element) {

      if(!isNaN(element) || element === '.'){
        this.calculatorValue += element + ''
      }

      if(element === 'C'){
        this.calculatorValue = ''
      }

      if(element === '%'){
        this.calculatorValue = this.calculatorValue / 100 + ''
      }

      if(['/', '*', '-', '+'].includes(element)){
        this.operator = element
        this.previousCalculatorValue = this.calculatorValue
        this.calculatorValue = ''
      }

      if(element === '='){
        this.calculatorValue = eval(
          this.previousCalculatorValue + this.operator + this.calculatorValue
        )

        this.previousCalculatorValue = '',
        this.operator = null
      }

    } 
  }
};
</script>

<style scoped>
.bg-vue-dark {
  background: #31475e;
}
.hover-class:hover {
  cursor: pointer;
  background: #3d5875;
}
.bg-vue-green {
  background: #3fb984;
}
</style>
