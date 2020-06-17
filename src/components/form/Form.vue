<template>
  <form class="container" @submit="onSubmit">
    <CreditCard
      :cardNumber="cardNumber"
      :cardName="cardName"
      :monthSelected="monthSelected"
      :yearSelected="yearSelected"
      :cvv="cvv"
      :mask="mask"
    />
    <label for="card-number">Card Number</label>
    <input
      v-model="cardNumber"
      v-mask="mask"
      class="input w100 mb15"
      type="text"
      id="card-number"
    />
    <label for="card-name">Card Name</label>
    <input v-model="cardName" class="input w100 mb15" type="text" id="card-name" />
    <div class="bottom-inputs w100 mb15">
      <div class="exp-date-container">
        <label for="exp-date">Expiration Date</label>
        <div class="exp-date-inputs">
          <select class="input mr15" name="month" id="exp-date" v-model="monthSelected">
            <option value="MM" disabled>Month</option>
            <option v-for="month in months" :value="month" :key="month">{{ month }}</option>
          </select>
          <select class="input" name="year" id="exp-date" v-model="yearSelected">
            <option value="YY" disabled>Year</option>
            <option v-for="year in years" :value="year" :key="year">{{ year }}</option>
          </select>
        </div>
      </div>
      <div class="cvv-container">
        <label for="cvv">CVV</label>
        <input v-model="cvv" class="input" type="text" id="cvv" />
      </div>
    </div>
    <button class="w100 submit">Submit</button>
  </form>
</template>

<script>
import CreditCard from './credit-card/CreditCard.vue';

export default {
  components: {
    CreditCard,
  },
  data() {
    return {
      cardNumber: '',
      cardName: '',
      monthSelected: 'MM',
      months: ['01', '02', '03', '04', '05', '06', '07', '08', '09', '10', '11', '12'],
      yearSelected: 'YY',
      years: [],
      cvv: '',
      mask: '#### #### #### ####',
    };
  },
  mounted() {
    let year = new Date().getFullYear();

    for (let i = 0; i < 20; i += 1) {
      this.years.push(year.toString());
      year += 1;
    }
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();
    },
  },
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
  padding-top: 125px;
  padding-left: 25px;
  padding-right: 25px;
  padding-bottom: 25px;
  background-color: white;
  border-radius: 10px;
  width: 400px;
  -webkit-box-shadow: 0px 0px 10px 1px rgba(0, 0, 0, 0.21);
  -moz-box-shadow: 0px 0px 10px 1px rgba(0, 0, 0, 0.21);
  box-shadow: 0px 0px 10px 1px rgba(0, 0, 0, 0.21);
}

.bottom-inputs {
  display: flex;
  justify-content: space-between;
  width: 100%;
}

label {
  font-size: 0.7rem;
  align-self: flex-start;
}

.submit {
  padding: 10px;
  border-radius: 5px;
  border: none;
  background-color: rgb(67, 86, 255);
  color: white;
}

.w100 {
  width: 100%;
}

.mb15 {
  margin-bottom: 15px;
}

.mr15 {
  margin-right: 15px;
}

.input {
  padding: 10px;
  border-radius: 5px;
  border: 1px solid;
  border-color: #ddd;
  transition: border-color 0.25s ease-in;
}

.input:focus {
  outline: none;
  border: 1px solid;
  border-color: rgb(71, 89, 255);
}

.input:hover {
  border: 1px solid rgb(71, 89, 255);
}

.exp-date-container {
  display: flex;
  flex-direction: column;
  width: 60%;
}

.exp-date-inputs {
  display: flex;
}

.exp-date-inputs select {
  width: 50%;
}

.cvv-container {
  display: flex;
  flex-direction: column;
  width: 30%;
}
</style>
