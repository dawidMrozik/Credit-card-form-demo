<template>
  <div class="card-container">
    <div class="card-imgs">
      <img class="chip-img" src="@/assets/chip.png" alt="chip" />
      <img class="provider-img" src="@/assets/visa.png" alt="visa" />
    </div>
    <div class="credit-card-number">
      <span
        v-for="(number, index) in maskedCardNumber"
        :key="index"
        aria-hidden="true"
        class="number"
        >{{ number }}</span
      >
    </div>
    <div class="card-bottom">
      <div class="credit-card-name-container">
        <label for="creditCardName">Card Holder</label>
        <div class="credit-card-name" id="creditCardName">{{ shortenCardName }}</div>
      </div>
      <div class="credit-card-expiration-date-container">
        <label for="credit-card-expiration-date">Expires</label>
        <div id="credit-card-expiration-date" class="expires">
          {{ monthSelected }} / {{ shortenYearSelected }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    cardNumber: String,
    cardName: String,
    monthSelected: String,
    yearSelected: String,
    cvv: String,
    mask: String,
  },
  data() {
    return {};
  },
  computed: {
    maskedCardNumber() {
      return this.cardNumber + this.mask.slice(this.cardNumber.length);
    },
    shortenCardName() {
      const MAX_CARD_NAME_LENGTH = 20;

      if (this.cardName.length > MAX_CARD_NAME_LENGTH) {
        const shorterName = `${this.cardName.slice(0, MAX_CARD_NAME_LENGTH)}...`;
        return shorterName;
      }

      return this.cardName;
    },
    shortenYearSelected() {
      return this.yearSelected === 'YY' ? this.yearSelected : this.yearSelected.slice(2);
    },
  },
};
</script>

<style scoped>
.card-container {
  font-family: 'Sans Code Pro', sans-serif;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  position: absolute;
  top: -100px;
  width: 310px;
  height: 190px;
  background: url(../../../assets/bg.jpeg);
  background-size: cover;
  border-radius: 10px;
  color: white;
  padding: 20px;
  -webkit-box-shadow: 0px 0px 53px 1px rgba(0, 0, 0, 0.6);
  -moz-box-shadow: 0px 0px 53px 1px rgba(0, 0, 0, 0.6);
  box-shadow: 0px 0px 53px 1px rgba(0, 0, 0, 0.6);
}

.card-imgs {
  display: flex;
  justify-content: space-between;
}

.card-bottom {
  display: flex;
  justify-content: space-between;
}

.card-bottom label {
  font-size: 0.6rem;
}

.provider-img {
  height: 30px;
}

.chip-img {
  height: 30px;
}

.credit-card-number {
  font-size: 1.6rem;
}

.number {
  position: relative;
  transform: translateY(100px);
}

.credit-card-name-container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: flex-start;
}

.credit-card-expiration-date-container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: flex-end;
}
</style>
