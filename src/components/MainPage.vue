<template>
  <div>
    <p class="title text-5xl font-bold">Mana Lagi Berbaloi?</p>
  </div>
  <div class="flex flex-row justify-content-around product-container gap-5">
    <div class="product1Container flex flex-column align-items-start product">
      <div class="flex w-full justify-content-center">
        <h2 class="product-title">Product 1</h2>
      </div>
      <div class="p-field">
        <label for="quantity1">Quantity</label>
        <InputNumber
          v-model="quantity1val"
          inputId="quantity1"
          fluid
        ></InputNumber>
      </div>
      <div class="p-field">
        <label for="volume1">Volume</label>
        <InputNumber v-model="volume1val" id="volume1" fluid></InputNumber>
      </div>
      <div class="p-field">
        <label for="price1">Price</label>
        <InputNumber v-model="price1val" id="price1" fluid></InputNumber>
      </div>
      <div class="p-field">
        <label for="value1">Value</label>
        <InputNumber
          v-model="value1val"
          id="value1"
          disabled
          class="border-1 pl-2 border-round-sm py-1"
          fluid
        ></InputNumber>
      </div>
    </div>

    <div class="product2Container flex flex-column align-items-start product">
      <div class="flex w-full justify-content-center">
        <h2 class="product-title">Product 2</h2>
      </div>
      <div class="p-field">
        <label for="quantity2">Quantity</label>
        <InputNumber id="quantity2" v-model="quantity2val" fluid />
      </div>
      <div class="p-field">
        <label for="volume2">Volume</label>
        <InputNumber v-model="volume2val" id="volume2" fluid></InputNumber>
      </div>
      <div class="p-field">
        <label for="price2">Price</label>
        <InputNumber v-model="price2val" id="price2" fluid></InputNumber>
      </div>
      <div class="p-field">
        <label for="value1">Value</label>
        <InputNumber
          v-model="value2val"
          id="value2"
          disabled
          fluid
          class="border-1 border-round-sm pl-2 py-1"
        ></InputNumber>
      </div>
    </div>
  </div>

  <div class="button-container flex flex-row gap-3 justify-content-center">
    <div
      class="calculate-container flex border-2 border-round-sm border-400 p-2"
    >
      <Button label="Calculate" @click="calculate" />
    </div>
    <div class="reset-container flex border-2 border-round-sm border-400 p-2">
      <Button label="Reset" @click="reset" />
    </div>
  </div>

  <div class="result-container">
    <p>Result:</p>
    <p :class="{ 'animate-result': animate }">{{ result }}</p>
  </div>
</template>

<script>
import InputNumber from "primevue/inputnumber";
import Button from "primevue/button";

export default {
  components: {
    InputNumber,
    Button,
  },
  data() {
    return {
      quantity1val: 1,
      volume1val: 1,
      price1val: 0,
      quantity2val: 1,
      volume2val: 1,
      price2val: 0,
      value1val: 0,
      value2val: 0,
      result: "",
      animate: false,
    };
  },
  methods: {
    // TODO: users can choose if they want 1 or many comparison

    calculate() {
      this.animate = true;
      setTimeout(() => {
        this.animate = false;
      }, 1000); // Duration of the animation

      if (
        this.quantity1val <= 0 ||
        this.volume1val <= 0 ||
        this.price1val <= 0
      ) {
        this.result = "Please fill in all fields with valid values";
        return;
      } else {
        this.value1val = this.price1val / (this.quantity1val * this.volume1val);
      }

      if (
        this.quantity2val <= 0 ||
        this.volume2val <= 0 ||
        this.price2val <= 0
      ) {
        this.result = "Please fill in all fields with valid values";
        return;
      } else {
        this.value2val = this.price2val / (this.quantity2val * this.volume2val);
      }

      if (isNaN(this.value1val) || isNaN(this.value2val)) {
        this.result = "Please fill in all fields with valid values";
      } else {
        this.result =
          this.value1val === this.value2val
            ? "Both equally berbaloi"
            : this.value1val > this.value2val
            ? "Product 2 is cheaper"
            : "Product 1 is cheaper";
      }
    },
    reset() {
      this.quantity1val = 1;
      this.volume1val = 1;
      this.price1val = 0;
      this.quantity2val = 1;
      this.volume2val = 1;
      this.price2val = 0;
      this.value1val = 0;
      this.value2val = 0;
      this.result = "";
    },
  },
};
</script>

<style scoped>
.title {
  text-align: center;
  color: brown;
}

.product-container {
  padding: 20px;
  border-width: 20px;
  /* flex-wrap: wrap; */
  background-color: rgb(255, 247, 236);
}

.product-title {
  color: brown;
}

.product {
  border: 1px solid #3333;
  padding: 20px;
  border-radius: 8px;
  margin-bottom: 20px;
  border-width: 5px;
}

.product h2 {
  margin-bottom: 10px;
}

.p-field {
  margin-bottom: 20px;
  color: brown;
}

.button-container {
  text-align: center;
  margin-top: 20px;
  color: #000;
  border-width: 2px;
}

.result-container {
  text-align: center;
  margin-top: 20px;
  font-size: 1.2em;
  font-weight: bold;
  color: brown;
}

.animate-result {
  transition: transform 1s, opacity 1s;
  transform: scale(1.1);
  opacity: 0.5;
}

/* @media (max-width: 500px) {
  .product-container {
    flex-direction: column;
  }
} */
</style>
