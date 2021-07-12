<template>
  <div class="container">
    <div class="inp">
      <input
      v-model="display"
      v-on:keyup.enter="operation"
      >
      <button class="clear"
      v-on:click="clear">clear</button>
    </div>
    <div class="keys">
      <div class="numerals">
        <div
          v-for="number in numbers"
          :key="number"
          v-on:click="num(number)">{{ number }}</div>
        <button class="submit"
        v-on:click="operation">=</button>
      </div>
      <div class="actions">
        <div
          v-for="(action, index) in actions"
          :key="index"
          v-on:click="num(action.type)">{{ action.type }}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calc',
  data() {
    return {
      display: '',
      temp: '',
      numbers: ['1', '2', '3', '4', '5', '6', '7', '8', '9', '.', '0'],
      actions: [
        {
          type: '+',
          method: 'sum',
        }, {
          type: '-',
          method: 'subtraction',
        }, {
          type: ':',
          method: 'divide',
        }, {
          type: 'x',
          method: 'multiply',
        }
      ]
    }
  },
  methods: {
    operation: function() {
      this.actions.forEach(action => {
        if (this.display.indexOf(action.type) !== -1) {
          let arr = this.display.split(action.type);
          this.display = String(this[action.method](arr));
        }
      });
    },
    clear: function() {
      this.display = '';
    },
    num: function(num) {
      this.display += num;
    },
    multiply: numb => {
      return numb.reduce((a, b) => a * b);
    },
    divide: numb => {
      return numb.reduce((a, b) => a / b);
    },
    sum: numb => {
      return numb.reduce((a, b) => Number(a) + Number(b));
    },
    subtraction: numb => {
      numb.forEach((item, index) => {
        if (!item) {
          numb[index + 1] = -numb[index + 1];
        }
      });
      numb = numb.filter(el => !!el);
      return numb.reduce((a, b) => a - b);
    }
  }
}
</script>

<style>
body {
  background:
  linear-gradient(225deg, transparent 24.5%, #449CB4 24.6%, transparent 24.8%) 37px -37px, 
  linear-gradient(135deg, transparent 24.5%, #449CB4 24.6%, transparent 24.8%) 37px 111px, 
  linear-gradient(135deg, transparent 24.5%, #449CB4 24.6%, transparent 24.8%) 37px 37px, 
  linear-gradient(225deg, transparent 24.5%, #449CB4 24.6%, transparent 24.8%) 37px 37px, 
  linear-gradient(135deg, transparent 24.5%, #449CB4 24.6%, transparent 24.8%) 74px 0px, 
  linear-gradient(225deg, transparent 24.5%, #449CB4 24.6%, transparent 24.8%) 74px 0px, 
  linear-gradient(135deg, transparent 24.5%, #449CB4 24.6%, transparent 24.8%) 74px 74px, 
  linear-gradient(225deg, transparent 24.5%, #449CB4 24.6%, transparent 24.8%) 74px 74px;
  background-size: 148px 148px;
  background-color: #E8F4F2;
}
.container{
  width: 400px;
  border: 1px solid black;
  margin: 50px auto;
  background: rgba(67, 147, 182, 0.425);
  border-radius: 5px;
}

.inp {
  display: flex;
  padding: 10px 10px;
  height: 75px;
}

.inp input {
  width: 100%;
  font-size: 30px;
  padding-left: 10px;
  font-family: 'Orbitron', sans-serif;
  background: rgba(7, 170, 219, 0.753);
}


.inp button {
  width: 98px;
  height: 75px;
  font-family: 'Orbitron', sans-serif;
  font-size: 20px;
  border-radius: 0 2px 2px 0;
  border: 1px solid;
  cursor:pointer;
}

.keys {
  display: flex;
  display: flex;
  justify-content: space-between;
  padding: 5px;
  font-family: 'Orbitron', sans-serif;
  font-size: 25px;
}

.numerals {
  display: flex;
  flex-wrap: wrap;
}

.numerals button {
  margin: 0;
  padding: 0;
  background: none;
  width: 77px;
  height: 77px;
  font-size: 30px;
  border: 1px solid black;
  border-radius: 2px;
  margin: 5px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor:pointer;
  background: rgba(255, 102, 0, 0.781);
}

.numerals div {
  width: 75px;
  height: 75px;
  border: 1px solid black;
  margin: 5px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor:pointer;
  background: rgba(59, 59, 59, 0.678);
  border-radius: 2px;
}

.numerals div {
  -webkit-transition: box-shadow 300ms ease-in-out, color 300ms ease-in-out;
  transition: box-shadow 300ms ease-in-out, color 300ms ease-in-out;
}
.numerals div:hover {
  box-shadow: 0 0 40px 40px #ff4800c2 inset;
}

.actions {
  display: flex;
  flex-direction: column;
}

.actions div {
  width: 75px;
  height: 75px;
  border: 1px solid black;
  border-radius: 2px;
  margin: 5px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: 'Orbitron', sans-serif;
  font-size: 25px;
  cursor:pointer;
  background: rgba(255, 255, 255, 0.781);
}

.actions div {
  -webkit-transition: box-shadow 300ms ease-in-out, color 300ms ease-in-out;
  transition: box-shadow 300ms ease-in-out, color 300ms ease-in-out;
}
.actions div:hover {
  box-shadow: 0 0 40px 40px #0084ffad inset;
}
</style>