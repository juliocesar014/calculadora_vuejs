<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <div class="col-md-4 m-3">
      <table class="table table-bordered">
        <tbody>
          <tr class="output">
            <td colspan="4">
              {{ output || 0 }}
            </td>
          </tr>
          <tr>
            <td v-on:click="clearField">C</td>
            <td v-on:click="setNegativeOrPositive">+/-</td>
            <td v-on:click="calculatorPorcentage">%</td>
            <td class="operadores" @click="processOutput('div')"><i class="fas fa-divide"></i></td>
          </tr>
          <tr>
            <td v-on:click="getNumber('7')">7</td>
            <td v-on:click="getNumber('8')">8</td>
            <td v-on:click="getNumber('9')">9</td>
            <td class="operadores" @click="processOutput('multi')"><i class="fa-solid fa-xmark"></i></td>
          </tr>
          <tr>
            <td v-on:click="getNumber('4')">4</td>
            <td v-on:click="getNumber('5')">5</td>
            <td v-on:click="getNumber('6')">6</td>
            <td class="operadores" @click="processOutput('sub')"><i class="fa-solid fa-minus"></i></td>
          </tr>
          <tr>
            <td v-on:click="getNumber('1')">1</td>
            <td v-on:click="getNumber('2')">2</td>
            <td v-on:click="getNumber('3')">3</td>
            <td class="operadores" @click="processOutput('add')"><i class="fa-solid fa-plus"></i></td>
          </tr>
          <tr>
            <td colspan="2" v-on:click="getNumber('0')">0</td>
            <td v-on:click="getDot()">.</td>
            <td class="operadores" @click="updateOutput"><i class="fa-solid fa-equals"></i></td>
          </tr>
        </tbody>
      </table>
    </div>


  </div>
</template>

<script>

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      output: '',
      previousValue: null,
      operationFired: false,
    }
  },
  methods: {
    clearField() {
      this.output = '';
    },
    setNegativeOrPositive() {
      this.output = this.output[0] === '-' ? this.output.slice(1) : `-${this.output}`;
    },
    calculatorPorcentage() {
      this.output = parseFloat(this.output) / 100;
    },
    getNumber(number) {

      if (this.operationFired) {
        this.output = '';
        this.operationFired = false;
      }







      this.output = `${this.output}${number}`;
    },
    getDot() {
      if (this.output.indexOf('.') === -1) {
        this.output = this.output + '.';
      }
    },
    processOutput(string) {

      if (string == 'add') {
        this.operation = (a, b) => {
          return parseFloat(a) + parseFloat(b);
        }
      } else if (string == 'sub') {
        this.operation = (a, b) => {
          return parseFloat(a) - parseFloat(b);
        }
      } else if (string == 'multi') {
        this.operation = (a, b) => {
          return parseFloat(a) * parseFloat(b);
        }
      } else if (string == 'div') {
        this.operation = (a, b) => {
          return parseFloat(a) / parseFloat(b);
        }
      }




      this.previousValue = this.output;
      this.operationFired = true;
    },
    updateOutput() {
      this.output = `${this.operation(this.previousValue, this.output)}`;
      this.previousValue = null;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Dancing+Script&display=swap');

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

h1 {
  font-family: 'Dancing Script', cursive;
  font-size: 2.5rem;
  color: #333;
}

.output {
  background-color: #333;
  color: #fff;
}

.operadores {
  background-color: orange;
  color: #fff;
}


.operadores:active {
  background-color: #333;
  color: #fff;
}
</style>

