<template>
  <div class="Icalc">
    <div class="display"> <div class="visible_element"> {{current || '0'}}</div> </div>
    <div @click="clear" class="btn"> <div class="visible_element"> C </div></div>
    <div @click="sign" class="btn"> <div class="visible_element"> +/- </div></div>
    <div @click="mod" class="btn"> <div class="visible_element"> % </div></div>
    <div @click="divide" class="btn operator"> <div class="visible_element"> ÷</div></div>
    <div @click="append('7')" class="btn"> <div class="visible_element"> 7 </div></div>
    <div @click="append('8')" class="btn"> <div class="visible_element"> 8 </div></div>
    <div @click="append('9')" class="btn"> <div class="visible_element"> 9 </div></div>
    <div @click="times" class="btn operator"> <div class="visible_element"> *</div></div>
    <div @click="append('4')" class="btn"> <div class="visible_element"> 4 </div></div>
    <div @click="append('5')" class="btn"> <div class="visible_element"> 5 </div></div>
    <div @click="append('6')" class="btn"> <div class="visible_element"> 6 </div></div>
    <div @click="minus" class="btn operator"> <div class="visible_element"> - </div></div>
    <div @click="append('1')" class="btn"> <div class="visible_element"> 1 </div></div>
    <div @click="append('2')" class="btn"> <div class="visible_element"> 2 </div></div>
    <div @click="append('3')" class="btn"> <div class="visible_element"> 3 </div></div>
    <div @click="add" class="btn operator"> <div class="visible_element"> +</div></div>
    <div @click="append('0')" class="btn zero"> <div class="visible_element"> 0</div></div>
    <div @click="dot" class="btn"> <div class="visible_element"> . </div></div>
    <div @click="equal" class="btn operator"> <div class="visible_element"> =</div></div>
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
.Icalc {
  width: 320px;
  height: 534px;
  font-size: 30px;
  display: grid; /* Właczenie siatki */
  grid-template-columns: repeat(4, auto); /* Ustawienie siatki na cztery kolumny */
  grid-template-rows: repeat(6, 89px);

  z-index: 0;
}

.display {
  grid-column: 1 / 5;
  text-align: right;
  background-color: #cbe6ec;
}
.display .visible_element {
  padding-right: 22px;
}

.btn {
  background-color: #536570;
  border: 1px solid #242c31;
  cursor: pointer;
}
.btn :active {
  /*transform: scale(0.5); */
  transform: scale(0.9);
}

.operator {
  background-color: #cbe6ec;
  border: none;
}

.zero {
  grid-column: 1/3;
}

.visible_element {
  padding-top: 30px;
  z-index: 1;
}

</style>