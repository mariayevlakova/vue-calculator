<template>
 <div class="calculator">
   <div class="display">{{ output || '0'}}</div>
    <div class="btn op" @click="clear">AC</div>
    <div class="btn op" @click="sign">+/-</div>
    <div class="btn op" @click="percent">%</div>
    <div class="btn op" @click="divide">÷</div>
    <div class="btn" @click="append('7')">7</div>
    <div class="btn" @click="append('8')">8</div>
    <div class="btn" @click="append('9')">9</div>
    <div class="btn" @click="multiply">x</div>
    <div class="btn" @click="append('4')">4</div>
    <div class="btn" @click="append('5')">5</div>
    <div class="btn" @click="append('6')">6</div>
    <div class="btn op" @click="minus">-</div>
    <div class="btn" @click="append('1')">1</div>
    <div class="btn" @click="append('2')">2</div>
    <div class="btn" @click="append('3')">3</div>
    <div class="btn op" @click="add">+</div>
    <div class="btn zero" @click="append('0')">0</div>
    <div class="btn" @click="dot">.</div>
    <div class="btn op" @click="equal">=</div>
 </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      output: '',
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.output = '';
    },
     sign() {
       this.output = this.output.charAt(0) === '-' ? 
         this.output.slice(1) : `-${this.output}`;
     },
     percent() {
       this.output = `${parseFloat(this.output) / 100}`;
     },
     dot() {
       if (this.output.indexOf('.') === -1) {
         this.append('.');
       }
     },
      prevInput() {
       this.previous = this.output;
       this.operatorClicked = true;
     },
     divide() {
       this.operator = (a, b) => a / b;
       this.prevInput();
     },
     multiply() {
       this.operator = (a, b) => a * b;
       this.prevInput();
     },
     minus() {
       this.operator = (a, b) => a - b;
       this.prevInput();
     },
     add() {
       this.operator = (a, b) => a + b;
       this.prevInput();
    },
     equal() {
       this.output = `${this.operator(
         parseFloat(this.previous), 
         parseFloat(this.output)
       )}`;
       this.previous = null;
    },
    append(num) {
      if(this.operatorClicked) {
        this.output = '';
        this.operatorClicked = false;
      }
      this.output = `${this.output}${num}`;
    }
  }
}
</script>

<style scoped>
.calculator {
  display: grid;
  grid-auto-columns: repeat(4, 1fr);
  grid-gap: 15px;
  width: 400px;
  align-items: center;
  margin: 0 auto;
}
.display {
  grid-column: 1 / 5;
  text-align: right;
  border: 2px whitesmoke solid;
  font-size: 18px;
  width: 400px;
  padding: 15px;
}
.zero {
  grid-column: 1 / 3;
}
.btn {
  background-color:  rgb(161, 158, 158);
  border: none;
  font-size: 18px;
  cursor: pointer;
  padding: 15px;
} 
.op {
  background-color: rgb(166, 167, 111);
}
.btn:hover {
  background-color: rgb(136, 135, 135);
}
.op:hover {
  background-color: rgb(142, 143, 98); 
}

</style>


