<template>
  <div id="app">
    <div class="calculator">
      <div class="display"><center>{{ current || "0" }}</center></div>
      <button @click="clear()" class="btn"><center>C</center></button>
      <button @click="sign()" class="btn"><center>+/-</center></button>
      <button @click="percent()" class="btn"><center>%</center></button>
      <button @click="divide()" class="btn operator"><center>÷</center></button>
      <button @click="append('7')" class="btn"><center>7</center></button>
      <button @click="append('8')" class="btn"><center>8</center></button>
      <button @click="append('9')" class="btn"><center>9</center></button>
      <button @click="multiply()" class="btn operator"><center>×</center></button>
      <button @click="append('4')" class="btn"><center>4</center></button>
      <button @click="append('5')" class="btn"><center>5</center></button>
      <button @click="append('6')" class="btn"><center>6</center></button>
      <button @click="minus()" class="btn operator"><center>-</center></button>
      <button @click="append('1')" class="btn"><center>1</center></button>
      <button @click="append('2')" class="btn"><center>2</center></button>
      <button @click="append('3')" class="btn"><center>3</center></button>
      <button @click="plus()" class="btn operator"><center>+</center></button>
      <button @click="append('0')" class="zero btn"><center>0</center></button>
      <button @click="dot()" class="btn"><center>.</center></button>
      <button @click="equal()" class="btn operator"><center>=</center></button>
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      current: "",
      previous: null,
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.current = ""
    },
    sign() {
      // This replaces the character of the number at 1st place , if "", to -
      this.current = this.current.charAt(0) === "-" ?
          this.current.slice(1) : `-${this.current}`;
      // Slice removes "-" sign if it's there in the number
    },
    percent() {
      this.current = `${parseFloat(this.current) / 1000}`
      // This grabs the "current" item and converts into parseFloat() and divide into 1000
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      } else if (this.current === "NaN") {
        this.current = "";
      }
      this.current = `${this.current}${number}`
    },
    dot() {
      if (this.current.indexOf('.') === -1){
        this.append('.')
      } else {
        alert("Sorry! '.' already exists!")
      }
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    multiply() {
      this.operator = (a, b) => a * b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    plus() {
      this.operator = (a, b) => a + b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    equal() {
      this.current = `${this.operator(
          parseFloat(this.current),
          parseFloat(this.previous)
      )}`;
      this.previous = null;
    }
  }
}
</script>

<style scoped>

#app {
  max-width: 500px;
  margin: auto;
}

.calculator {
  display: grid;
  padding: 50px;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  font-size: 40px;
}

.calculator .display {
  grid-column: 1 / 5;
  background: #333;
  color: white;
}

.zero {
  grid-column: 1 / 3;
}

.btn {
  background-color: #eee;
  border: 1px solid #999;
  align-items: center;
  font-size: 40px;
}

.btn:hover {
  background-color: rgba(86,86,86,0.79);
}

.operator {
  background-color: orange;
  color: white;
}

</style>
