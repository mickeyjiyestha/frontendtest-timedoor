<script setup>
import pizzaList from "@/assets/json/pizza-list.json";
import toppingList from "@/assets/json/topping-list.json";
import sizeList from "@/assets/json/size-list.json";
import { ref, computed, onMounted, watch } from "vue";
import CheesePizza from "@/assets/img/pizza/CheesePizza.png";
import VeggiePizza from "@/assets/img/pizza/VeggiePizza.png";
import ClassicalPizza from "@/assets/img/pizza/ClassicalPizza.png";

const pizzas = ref([]);
const sizes = ref([]);
const selectedSize = ref(null);
const pizzaToppings = ref([]);
const selectedToppings = ref([]);
const selectedPizza = ref(null);
const isModalOpen = ref(false);

function getPizzaImage(name) {
  switch (name) {
    case "Cheese Pizza":
      return CheesePizza;
    case "Veggie Pizza":
      return VeggiePizza;
    case "Classical Pizza":
      return ClassicalPizza;
    default:
      return "";
  }
}

const availableToppings = computed(() => {
  if (!selectedPizza.value) {
    return pizzaToppings.value.map((t) => t.id);
  }
  const pizza = pizzas.value.find((p) => p.id === selectedPizza.value);
  return pizza ? pizza.toppings : [];
});

const selectedPizzaDetails = computed(() => {
  return pizzas.value.find((p) => p.id === selectedPizza.value) || null;
});

const selectedSizeDetails = computed(() => {
  return (
    sizes.value.find((s) => s.id === selectedSize.value) || { extra_price: 0 }
  );
});

const selectedToppingsDetails = computed(() => {
  return pizzaToppings.value.filter((t) =>
    selectedToppings.value.includes(t.id)
  );
});

const totalPrice = computed(() => {
  return (
    (selectedPizzaDetails.value?.price || 0) +
    selectedSizeDetails.value.extra_price +
    selectedToppingsDetails.value.reduce((total, t) => total + t.price, 0)
  );
});

const openModal = () => {
  isModalOpen.value = true;
};

const closeModal = () => {
  isModalOpen.value = false;
};

onMounted(() => {
  pizzas.value = pizzaList.data;
  pizzaToppings.value = toppingList.data;
  sizes.value = sizeList.data;
});

watch(selectedPizza, () => {
  selectedSize.value = null;
  selectedToppings.value = [];
});
</script>

<template>
  <div class="hero container">
    <p class="section-title">Choose Your Pizza</p>
    <div class="section-hero">
      <div class="pizza-options">
        <div>
          <div class="pizza-options">
            <label
              v-for="pizza in pizzas"
              :key="pizza.id"
              class="pizza-option"
              :class="{ selected: selectedPizza == pizza.id }"
            >
              <input
                type="radio"
                name="pizza-radio"
                :value="pizza.id"
                v-model="selectedPizza"
                style="display: none"
              />
              <div class="pizza-info">
                <img
                  :src="getPizzaImage(pizza.name)"
                  alt="Pizza Image"
                  width="100"
                  height="100"
                />
                <div class="text-info">
                  <h2>{{ pizza.name }}</h2>
                  <p>${{ pizza.price }}</p>
                </div>
              </div>
            </label>
          </div>

          <div class="topping">
            <p class="topping-title">Custom Pizza</p>
            <div>
              <p class="topping-size">size</p>
              <div class="pizza-sizes">
                <div class="pizza-size" v-for="size in sizes" :key="size.id">
                  <input
                    type="radio"
                    :value="size.id"
                    v-model="selectedSize"
                    id="size-{{ size.id }}"
                  />
                  <label :for="'size-' + size.id">{{ size.name }}</label>
                </div>
              </div>

              <div class="pizza-topping">
                <label
                  v-for="topping in pizzaToppings"
                  :key="topping.id"
                  class="topping-label"
                  :class="{
                    unavailable:
                      selectedPizza && !availableToppings.includes(topping.id),
                    selected: selectedToppings.includes(topping.id),
                  }"
                >
                  <input
                    type="checkbox"
                    :value="topping.id"
                    v-model="selectedToppings"
                    class="topping-checkbox"
                    style="display: none"
                    :disabled="
                      selectedPizza && !availableToppings.includes(topping.id)
                    "
                  />
                  {{ topping.name }}
                </label>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="payment">
        <p class="payment-title">Payment Summary</p>
        <div class="first-payment-details">
          <p class="detail-name">{{ selectedPizzaDetails?.name }}</p>
          <p class="detail-price">{{ selectedPizzaDetails?.price }}$</p>
        </div>
        <div class="sec-payment-details" v-if="selectedSize">
          <p class="detail-name">Size - {{ selectedSizeDetails.name }}</p>
          <p class="detail-price">{{ selectedSizeDetails.extra_price }}$</p>
        </div>

        <div
          class="sec-payment-details"
          v-for="topping in selectedToppingsDetails"
          :key="topping.id"
        >
          <p class="detail-name">{{ topping.name }}</p>
          <p class="detail-price">{{ topping.price }}$</p>
        </div>
        <div class="container-price">
          <p class="text-total-price">Total Price</p>
          <p class="total-price">{{ totalPrice }}$</p>
        </div>
        <button class="order" @click="openModal">Order Now</button>
      </div>
    </div>
  </div>
  <div v-if="isModalOpen" class="modal-overlay">
    <div class="modal">
      <img src="@/assets/img/icons/modal.png" alt="" />
      <h2>Order Success</h2>
      <p>
        Thank you, we have received your<br />
        order successfully.
      </p>
      <button class="close" @click="closeModal">Close</button>
    </div>
  </div>
  <div class="hr">
    <hr />
  </div>
</template>

<style scoped>
.section-hero {
  display: flex;
}

.hero {
  margin-top: 100px;
  margin-left: 100px;
}

.section-title {
  color: #e77e23;
  font-size: 40px;
  font-weight: 900;
}

.pizza-options {
  display: flex;
  gap: 30px;
  justify-content: space-between;
}

.pizza-option {
  display: flex;
  align-items: center;
  padding: 15px;
  border: 1px solid rgb(230, 227, 227);
  border-radius: 15px;
  cursor: pointer;
  transition: border-color 0.3s ease;
}

.pizza-option:hover {
  background-color: rgb(236, 194, 115);
}

img {
  object-fit: cover;
  border-radius: 15px;
  transition: transform 0.3s ease;
  width: 150px;
  height: 150px;
}

.topping {
  margin-top: 150px;
}

.topping-title {
  color: #e77e23;
  font-size: 40px;
  font-weight: 900;
}

.pizza-option.selected {
  background-color: #e77e23;
  color: white;
}

.pizza-option:hover img {
  transform: rotate(30deg);
}

.pizza-option.selected {
  border-color: green;
}

.pizza-option.selected .text-info h2,
.pizza-option.selected .text-info p {
  color: white;
}

.pizza-info {
  margin-left: 10px;
  display: flex;
  transition: background-color 0.3s ease;
}

.text-info {
  display: flex;
  flex-direction: column;
  margin-left: 15px;
}

.text-info h2 {
  margin: 0;
  margin-top: 40px;
  font-size: 24px;
  color: #333;
}

.pizza-sizes {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.pizza-size {
  display: flex;
  gap: 15px;
  align-items: center;
}

.text-info p {
  margin: 5px 0 0;
  font-size: 16px;
  color: #555;
}

.payment {
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  padding: 20px;
  max-width: 400px;
  width: 100%;
  height: 80%;
  max-height: 500px;
  margin-left: 50px;
}

.payment-title {
  color: #e77e23;
  font-size: 20px;
  font-weight: 700;
}

.first-payment-details {
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: grey;
  margin-bottom: -30px;
}

.sec-payment-details {
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: grey;
  margin-bottom: -30px;
}

.detail-name {
  font-size: 19px;
}

.detail-price {
  color: black;
}

.topping-name {
  display: flex;
  justify-content: space-between;
}

.pizza-topping {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  gap: 10px;
  margin-top: 20px;
}

.topping-label {
  padding: 10px 15px;
  border: 2px solid rgb(230, 227, 227);
  border-radius: 30px;
  cursor: pointer;
  transition: all 0.3s ease;
  display: inline-block;
}

.topping-label:hover {
  background-color: #e77e23;
  color: white;
}

.topping-checkbox:checked + .topping-label {
  background-color: green;
  color: white;
  border-color: green;
}

.topping-label.unavailable {
  background-color: rgb(219, 215, 215);
  pointer-events: none;
  color: rgb(119, 118, 118);
}

.topping-checkbox.selected {
  background-color: #e77e23;
}

.topping-label.selected {
  background-color: #e77e23;
}

.container-price {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 60px;
}

.total-price {
  color: #e77e23;
  font-size: 20px;
  font-weight: 700;
}

.text-total-price {
  color: black;
  font-size: 23px;
}

.order {
  display: block;
  width: 100%;
  text-align: center;
  background-color: #e77e23;
  border: none;
  padding: 20px;
  border-radius: 40px;
  color: white;
  font-size: 20px;
}

.close {
  display: block;
  width: 100%;
  text-align: center;
  background-color: #e77e23;
  border: none;
  padding: 20px;
  border-radius: 40px;
  color: white;
  font-size: 20px;
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  background: white;
  padding: 20px;
  border-radius: 8px;
  text-align: center;
  width: 300px;
}

.hr {
  padding: 0 100px;
  margin-top: 150px;
  color: #c4c4c4;
}
</style>
