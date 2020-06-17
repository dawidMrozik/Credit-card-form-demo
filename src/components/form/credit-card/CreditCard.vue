<template>
  <div class="card-container">
    <div class="card-imgs">
      <img class="chip-img" src="@/assets/chip.png" alt="chip" />
      <img class="provider-img" src="@/assets/visa.png" alt="visa" />
    </div>
    <div class="credit-card-number">
      <span v-for="(n, index) in mask" :key="index">
        <transition name="slide-fade-up">
          <div
            v-if="cardNumber.length > index"
            class="numberItem"
            :class="{ '-active': n.trim() === '' }"
            :key="index"
          >{{ cardNumber[index] }}</div>
          <div
            v-else
            class="numberItem"
            :class="{ '-active': n.trim() === '' }"
            :key="index + 1"
          >{{ n }}</div>
        </transition>
      </span>
    </div>
    <div class="card-bottom">
      <div class="credit-card-name-container">
        <label for="creditCardName">Card Holder</label>
        <transition name="slide-fade-up">
          <div v-if="cardName.length > 0" key="1" class="credit-card-name" id="creditCardName">
            <transition-group name="slide-fade-right">
              <span
                class="card-item__nameItem"
                v-for="(n, index) in noWhitespacesCardName"
                :key="index + 1"
              >{{n}}</span>
            </transition-group>
          </div>
          <div v-else key="2" class="credit-card-name" id="creditCardName">FULL NAME</div>
        </transition>
      </div>
      <div class="credit-card-expiration-date-container">
        <label for="credit-card-expiration-date">Expires</label>
        <div id="credit-card-expiration-date" class="expires">
          <transition name="slide-fade-up">
            <span v-if="monthSelected" v-bind:key="monthSelected">{{monthSelected}}</span>
          </transition>
          <span class="credit-card-date-separator">/</span>
          <transition name="slide-fade-up">
            <span
              v-if="shortenYearSelected"
              v-bind:key="shortenYearSelected"
            >{{shortenYearSelected}}</span>
          </transition>
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
    noWhitespacesCardName() {
      return this.shortenCardName.replace(/\s\s+/g, ' ');
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
  font-weight: 500;
  line-height: 1;
  color: #fff;
  font-size: 27px;
  display: inline-block;
  cursor: pointer;
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

.credit-card-date-separator {
  display: inline-block;
  width: 10px;
}

.numberItem {
  font-size: 1.5rem;
  width: 14px;
  display: inline-block;
}

.numberItem-active {
  width: 24px;
}

.slide-fade-up-enter-active {
  transition: all 0.25s ease-in-out;
  transition-delay: 0.1s;
  position: relative;
}

.slide-fade-up-leave-active {
  transition: all 0.25s ease-in-out;
  position: absolute;
}

.slide-fade-up-enter {
  opacity: 0;
  transform: translateY(15px);
  pointer-events: none;
}

.slide-fade-up-leave-to {
  opacity: 0;
  transform: translateY(-15px);
  pointer-events: none;
}

.slide-fade-right-enter-active {
  transition: all 0.25s ease-in-out;
  transition-delay: 0.1s;
  position: relative;
}
.slide-fade-right-leave-active {
  transition: all 0.25s ease-in-out;
  position: absolute;
}
.slide-fade-right-enter {
  opacity: 0;
  transform: translateX(10px) rotate(45deg);
  pointer-events: none;
}
.slide-fade-right-leave-to {
  opacity: 0;
  transform: translateX(-10px) rotate(45deg);
  pointer-events: none;
}
</style>
