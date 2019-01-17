<template>
  <div class="calculator mx-auto">
    <div class="display">{{current || '0'}}</div>
    <div @click="clear" class="btn backgray">C</div>
    <div @click="bracket" class="btn backgray">( )</div>
    <div @click="percent" class="btn backgray">%</div>
    <div @click="divide" class="btn operator backgray">÷</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="times" class="btn operator backgray">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="minus" class="btn operator backgray">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add" class="btn operator backgray">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="equal" class="btn operator equal">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: "",
      operator: null,
      operatorClicked: false
    };
  },
  methods: {
    clear() {
      this.current = "";
    },
    sign() {
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    times() {
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
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
      this.previous = null;
    },
    bracket() {
      this.current =
        this.current.charAt(0) === "("
          ? this.current.slice(1)
          : `(${this.current}`;
    }
  }
};
</script>

<style scoped>
.mx-auto {
  margin: 0 auto;
  text-align: right;
  cursor: pointer;
}
.calculator {
  width: 300px;
  font-size: 20px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(80px, auto);
}

.display {
  grid-column: 1 / 5;
  background: #fff;
  /* border: 1px solid #eee; */
  color: rgb(16, 154, 218);
}

.zero {
  /* grid-column: 1 / 3; */
}

.btn {
  display: flex;
  flex-direction: column;
  padding-top: 20px;
  background: #fff;
  border: 1px solid #eee;
  border-radius: 0;
  font-size: 25px;
  text-align: center;
  color: rgb(16, 154, 218);
}

.operator {
  /* background: green; */
  color: rgb(16, 154, 218);
}

.equal {
  background: green;
  color: #fff;
}
.cha {
  color: #333;
}
.backgray {
  background: #f8f9f9;
}
</style>
