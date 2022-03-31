<template>
  <div class="logo"><img src="./assets/images/logo.svg" alt="logo"></div>
  <div class="tip-calculator">
      <div class="left-side">
        <label for="">Bill</label> <br>
        <input type="number" class="input bill-input" v-model="billInput"> <br>
        
        <label for="">Select tip %</label>
        <div class="tip-choosen">
          <div class="tip" :class="{'active-tip': isActive}" @click.prevent="tipInputHandle" 
              v-for="(tip, index) in tips" :key="index">
            {{ tip }}%
          </div>
          <div><input type="number" placeholder="OTHER" class="tip-custom" v-model="tipOther"></div>
        </div>
        
        <div class="ppl-label">
          <label for="">Number of People</label>
          <label for="" class="error" v-if="pplInput <= 0">Can't be zero</label>
        </div>
        <input type="number" class="input ppl-input" v-model="pplInput">
      </div><!-- end left side -->
      
      <div class="result">
        <div class="tip-amount">
          <div class="text">
            <p>Tip Amount</p>
            <p class="person">/ person</p>
          </div>
          <div class="amount" id="tip-amount">${{ tipAmount }}</div>
        </div>

        <div class="total">
          <div class="text">
            <p>Total</p>
            <p class="person">/ person</p>
          </div>
          <div class="amount" id="total-amount">${{ totalAmount }}</div>
        </div>

        <div class="reset" @click="reset">RESET</div>
      </div> <!-- end result -->
    </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      billInput: 0,
      tips: [
        5, 10, 15, 20, 25
      ],
      tip: 0,
      tipOther: 0,
      pplInput: 0,
      isActive: false,
    }
  },
  methods: {
    tipInputHandle(e) {
      this.isActive = !this.isActive
      if(this.isActive == true) {
        this.tip = parseFloat(e.target.innerHTML)/100
      }
      console.log(e.target, this.tip, typeof(this.tip), this.tipAmount, typeof(parseFloat(this.tipAmount)))
    },

    reset() {
      this.billInput = 0;
      this.pplInput = 0;
      this.tip = null;
      this.tipOther = null
    }
  },

  computed: {
    tipAmount() {
      if(this.billInput != 0 && this.pplInput != 0) {
        if(!this.tipOther) {
          return ((this.billInput * this.tip)/this.pplInput).toFixed(2);
        }else{
          return ((this.billInput * (this.tipOther / 100)) /this.pplInput).toFixed(2);
        }
      }else {
        return 4.32;
      }
    },
    totalAmount() {
      return ((this.billInput + parseFloat(this.tipAmount)) / this.pplInput).toFixed(2);
    }
  }
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    height: 100vh;
    width: 100%;
    background-color: hsl(185, 41%, 84%);
    font-family: "Space Mono", monospace;
}

.logo {
    text-align: center;
    margin-top: 2rem;
    margin-bottom: 3rem;
}

.tip-calculator {
    width: 60vw;
    background-color: #fff;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    padding: 2rem;
    border-radius: 1.4rem 1.4rem 0 0;
    margin: 0 auto;
}

label {
    color: hsl(186, 14%, 43%);
    /* font-family: 700; */
    margin-bottom: 1rem;
}

input {
    border: none;
    outline: none;
    padding: 5px 20px 5px 5px;
    background-position: 17px 15px;
    background-repeat: no-repeat;
    background-color: hsl(185, 41%, 84%);
    text-align: right;
    font-size: 24px; /* may make input bigger */
}

.bill-input {
    background-image: url('./assets/images/icon-dollar.svg');
    margin-bottom: 36px;
}

.tip-choosen {
    margin-top: 0.7rem;
    display: grid;
    grid-template-columns: 95px 95px 95px;
    row-gap: 2em;
    column-gap: 1em;
    margin-bottom: 2rem;
}

.tip {
    background-color: hsl(183, 100%, 15%);
    color: #fff;
    height: 48px;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    font-size: 24px;
    border-radius: 4px;
    cursor: pointer;
}

.tip:hover {
  background-color: hsl(185, 41%, 84%);
  color: hsl(184, 14%, 56%);
}

.tip-custom{
    width: 95px;
    height: 48px;
    border-radius: 4px;
    text-align: right;
}

/* .active-tip {
    background-color: hsl(185, 41%, 84%);
  color: hsl(184, 14%, 56%);
} */

.ppl-label {
    display: flex;
    justify-content: space-between
}
.error {
    color: red;
    /* display: none; */
}

.ppl-input {
    background-image: url('./assets/images/icon-person.svg');
    margin-bottom: 2.4rem;
}

.result {
    background-color: hsl(183, 100%, 15%);
    color: #fff;
    padding: 39px 21px;
    border-radius: 12px;
    width: 50%;
    position: relative;
}

.tip-amount,
.total {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 5rem;
}

.person {
    font-size: 12px;
    color: hsl(189, 41%, 97%);
    font-weight: 700;
}

.amount {
    font-size: 28px;
    color: hsl(172, 67%, 45%);
    font-weight: 700;
}

.reset {
    text-align: center;
    font-weight: 700;
    color: hsl(183, 100%, 15%);
    background-color: hsl(172, 67%, 45%);
    padding: 8px;
    border-radius: 4px;
    cursor: pointer;
    position: absolute;
    bottom: 0;
    right: 0;
    left: 0;
    margin: 0 1.4rem 2.2rem 1.4rem;
}
</style>
