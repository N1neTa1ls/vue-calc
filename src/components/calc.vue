<template>
  <div class="container">
    <div class="inp">
      <input
      pattern="[0-9]{1,15}"
      v-model="display"
      v-on:keyup.enter="operation"
      >
      
      <button class="clear"
      v-on:click="clear">clear</button>
    </div>
    <div class="keys">
      <div class="numerals">
        <div v-on:click="num('1')">1</div>
        <div v-on:click="num('2')">2</div>
        <div v-on:click="num('3')">3</div>
        <div v-on:click="num('4')">4</div>
        <div v-on:click="num('5')">5</div>
        <div v-on:click="num('6')">6</div>
        <div v-on:click="num('7')">7</div>
        <div v-on:click="num('8')">8</div>
        <div v-on:click="num('9')">9</div>
        <div v-on:click="num('.')">.</div>
        <div v-on:click="num('0')">0</div>
        <button class="submit"
        v-on:click="operation">=</button>
      </div>
      <div class="actions">
        <div v-on:click="num('+')">+</div>
        <div v-on:click="num('-')">-</div>
        <div v-on:click="num('/')">:</div>
        <div v-on:click="num('*')">X</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calc',
  data() {
    return {
    display: "",
    temp: []
    }
  },
  methods: {
    operation: function() {
      this.display = (this.display.indexOf('+') > 0) 
      ? this.display.split('+').reduce((a, b) => Number(a) + Number(b)) :
      (this.display.indexOf(':') > 0 || this.display.indexOf("/") > 0)
      ? this.display.replace(/:/i, '/').split('/').reduce((a, b) => a / b) :
      (this.display.indexOf('*') > 0 || this.display.indexOf("x") > 0) 
      ? this.display.replace(/x/i, '*').split('*').reduce((a, b) => a * b) :
      (this.display.indexOf('-') > -1)
      ? this.display.split('-').reduce((a, b) => a - b) :
      this.display = ""
    },
    clear: function() {
      this.display = ""
      this.temp = []
    },
    num: function(num) {
      this.temp.push(num)
      this.display = this.temp.join('')
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