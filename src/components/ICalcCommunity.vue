<template>
  <div class="Icalc">

    <div class="display">
      <div class="visible_element"> {{current || '0'}} </div> 
    </div>
    
    <div class="top_operator">
      <button @click="clear" class="btn"><div class="visible_element"> C </div></button>
      <button @click="sign" class="btn"> <div class="visible_element"> +/- </div></button>
      <button @click="mod" class="btn"> <div class="visible_element"> % </div></button>
      <button @click="divide" class="btn"> <div class="visible_element"> ÷</div></button>
    </div>

    <div class="right_operator">
      <button @click="times" class="btn"> <div class="visible_element"> *</div></button>
      <button @click="minus" class="btn"> <div class="visible_element"> - </div></button>
      <button @click="add" class="btn"> <div class="visible_element"> +</div></button>
      <button @click="equal" class="btn"> <div class="visible_element"> =</div></button>
    </div>

    <div class="button">
      <button @click="append('7')" class="btn"> <div class="visible_element"> 7 </div></button>
      <button @click="append('8')" class="btn"> <div class="visible_element"> 8 </div></button>
      <button @click="append('9')" class="btn"> <div class="visible_element"> 9 </div></button>
      <button @click="append('4')" class="btn"> <div class="visible_element"> 4 </div></button>
      <button @click="append('5')" class="btn"> <div class="visible_element"> 5 </div></button>
      <button @click="append('6')" class="btn"> <div class="visible_element"> 6 </div></button>
      <button @click="append('1')" class="btn"> <div class="visible_element"> 1 </div></button>
      <button @click="append('2')" class="btn"> <div class="visible_element"> 2 </div></button>
      <button @click="append('3')" class="btn"> <div class="visible_element"> 3 </div></button>
      <button @click="append('0')" class="btn zero"> <div class="visible_element"> 0</div></button>
      <button @click="dot" class="btn"> <div class="visible_element"> . </div></button>
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
@import "static/style.css";
</style>