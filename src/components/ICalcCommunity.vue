<template>
  <div class="Icalc">

    <div class="menu" id="menu">
      <button class="left_nav"><i class="nav_icon">&#xe800;</i></button>
      <button class="center_nav"><i class="nav_icon">&#xe801;</i></button>
      <button class="right_nav"><i class="nav_icon">&#xe802;</i></button>
    </div>

    <div class="display">
      <button v-on:keydown="numadd" class="visible_element"> {{current || '0'}} </button> 
    </div>
    
    <div class="top_operator">
      <button @click="clear" class="btn">C </button>
      <button @click="sign" class="btn"> +/- </button>
      <button @click="mod" class="btn"> % </button>
      <button @click="divide" class="btn"> ÷ </button>
    </div>

    <div class="right_operator">
      <button @click="times" class="btn"> * </button>
      <button @click="minus" class="btn"> - </button>
      <button @click="add" class="btn"> + </button>
      <button @click="equal" class="btn"> = </button>
    </div>

    <div class="button">
      <button @click="append('7')" class="btn"> 7 </button>
      <button @click="append('8')" class="btn"> 8 </button>
      <button @click="append('9')" class="btn"> 9 </button>
      <button @click="append('4')" class="btn"> 4 </button>
      <button @click="append('5')" class="btn"> 5 </button>
      <button @click="append('6')" class="btn"> 6 </button>
      <button @click="append('1')" class="btn"> 1 </button>
      <button @click="append('2')" class="btn"> 2 </button>
      <button @click="append('3')" class="btn"> 3</button>
      <button @click="append('0')" class="btn zero"> 0</button>
      <button @click="dot" class="btn"> . </button>
    </div>
    
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.current = '';
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ?
        this.current.slice(1) : `-${this.current}`;
    },
    numadd: function(event) {
      if(event.key == "Delete" || event.key == "Backspace"){
        this.clear();
      }
      else if(event.key == "s"){
        this.sign();
      }
      else if(event.key == "%"){
        this.mod();
      }
      else if(event.key == "/"){
        this.divide();
      }
      else if(event.key == "7"){
        this.append("7");
      }
      else if(event.key == "8"){
        this.append("8");
      }
      else if(event.key == "9"){
        this.append("9");
      }
      else if(event.key == "*"){
        this.times();
      }
      else if(event.key == "4"){
        this.append("4");
      }
      else if(event.key == "5"){
        this.append("5");
      }
      else if(event.key == "6"){
        this.append("6");
      }
      else if(event.key == "-"){
        this.minus();
      }
      else if(event.key == "1"){
        this.append("1");
      }
      else if(event.key == "2"){
        this.append("2");
      }
      else if(event.key == "3"){
        this.append("3");
      }
      else if(event.key == "+"){
        this.add();
      }
      else if(event.key == "0"){
        this.append("0");
      }
      else if(event.key == "," || event.key == "." ){
        this.append(".");
      }
      else if(event.key == "Enter" || event.key == "="){
        this.equal();
      }
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPrevious(){
      this.previous = this.current;
      this.operatorClicked = true;
    },
    mod() {
      this.operator = (a, b) => a % b;
      this.setPrevious();
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    times(){
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current =  `${this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      )}`;
      this.previous = null;
    },
    squack: function(text){
      this.append(text)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "static/nav_bar.css";
@import "static/style.css";
</style>