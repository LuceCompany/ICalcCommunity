<template>
  <div class="Icalc">
    <div class="display"> {{current || '0'}}</div>
    <div @click="clear" class="btn"> C</div>
    <div @click="sign" class="btn"> +/-</div>
    <div @click="mod" class="btn"> %</div>
    <div @click="divide" class="btn operator"> ÷</div>
    <div @click="append('7')" class="btn"> 7</div>
    <div @click="append('8')" class="btn"> 8</div>
    <div @click="append('9')" class="btn"> 9</div>
    <div @click="times" class="btn operator"> X</div>
    <div @click="append('4')" class="btn"> 4</div>
    <div @click="append('5')" class="btn"> 5</div>
    <div @click="append('6')" class="btn"> 6</div>
    <div @click="minus" class="btn operator"> -</div>
    <div @click="append('1')" class="btn"> 1</div>
    <div @click="append('2')" class="btn"> 2</div>
    <div @click="append('3')" class="btn"> 3</div>
    <div @click="add" class="btn operator"> +</div>
    <div @click="append('0')" class="btn zero"> 0</div>
    <div @click="dot" class="btn"> .</div>
    <div @click="equal" class="btn operator"> =</div>
  </div>
</template>

<script>
export default {
  /* document.keypress(function(){
    if(event.which == 46){
      this.methods.append('.');
    }
    else if (event.which == 45){
      this.method.append('0');
    }
  }, */
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
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.Icalc {
  width: 320px;
  height: 534px;
  font-size: 32px;
  display: grid; /* Właczenie siatki */
  grid-template-columns: repeat(4); /* Ustawienie siatki na cztery kolumny */
}

.display {
  grid-column: 1 / 5;
  text-align: right;
  background-color: #9dcbd6;
}

.btn {
  background-color: #536570;
  border: 1px solid #354149;
  cursor: pointer;
}
.btn.active {
  /*transform: scale(0.5); */
  background-color: #151a1d;
}

.operator {
  background-color: rgba(255, 60, 0, 0.918);
}

.zero {
  grid-column: 1/3;
}

</style>