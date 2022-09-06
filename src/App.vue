<template>
  <h1>{{ name }}</h1>
  <input type="text" v-model="name" />
  <button @click="placeOrder">Place order</button>
  <button @click="removeWatcher">Hide cart Alerts</button>
  <br /><br />
  <label for="selectCurrencySymbol">Currency</label>
  <select id="selectCurrencySymbol" v-model="currencySymbol">
    <option value="$">Dollars ($)</option>
    <option value="CHF">Franken (CHF)</option>
  </select>
  <YummyMeal
    v-for="meal in meals"
    :name="meal.name"
    :price="meal.price"
    @addToCart="addItemToCart"
  />
</template>

<script setup>
import YummyMeal from './components/YummyMeal.vue';
import { ref, reactive, watch, provide } from 'vue';

const currencySymbol = ref('$');
provide('currencySymbol', currencySymbol);

const name = ref('The Snazzy Burger');
const cart = reactive([]);
const meal = reactive({ name: 'Hamburger', price: 5 });
const meals = reactive([
  { name: 'Hamburger 🍔', price: 5 },
  { name: 'Cheeseburger 🧀', price: 6 },
  { name: 'Impossible Burge 🥕', price: 7 },
  { name: 'Fries 🍟', price: 2 },
]);
const placeOrder = () => {
  alert('Your order has been placed!');
};
const addItemToCart = (item) => cart.push(item);
const removeWatcher = watch(
  () => [...cart],
  (newValue, oldValue) => alert(newValue.join('\n'))
);
</script>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
