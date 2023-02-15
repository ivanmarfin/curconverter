<template>
  <div>
    <div class="converter">
      <input type="number" @input="onInputChange" :value="value">
      <select @change="onChangeFrom" :value="from">
        <option
            v-for="currency of currencies"
            :key="currency"
        >
          {{ currency }}
        </option>
      </select>
      <p>в</p>
      <select @change="onChangeTo" :value="to">
        <option
            v-for="currency of currencies"
            :key="currency"
        >
          {{ currency }}
        </option>
      </select>
      <button @click="onClickConvert">Конвертировать</button>
    </div>
    <p>{{ result }}</p>
  </div>
</template>

<script>
import {CurrencyService} from "@/services/CurrencyService";

export default {
  data() {
    return {
      service: new CurrencyService(),
      value: 0,
      from: 'USD',
      to: 'USD',
      currencies: [],
      result: ''
    }
  },
  async mounted() {
    this.currencies = await this.service.getCurrency()
  },
  methods: {
    onInputChange (event) {
      this.result = '';
      this.value = +event.target.value;
    },
    onChangeFrom (event) {
      this.result = '';
      this.from = event.target.value;
    },
    onChangeTo (event) {
      this.result = '';
      this.to = event.target.value;
    },
    async onClickConvert () {
      const result = await this.service.convert(
          this.value,
          this.from,
          this.to
      )
      this.result = `${this.value} ${this.from} равна ${result} ${this.to}`
    }
  }
}
</script>

<style>
.converter {
  display: flex;
  align-items: center;
  margin: 0 auto;
  width: max-content;
}
</style>
