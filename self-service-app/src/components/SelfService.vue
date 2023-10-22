<script setup lang="ts">

import { reactive } from 'vue';

interface ProductsProps {
  id: number,
  photo: string;
  name: string;
  price: number;
  active: boolean;
  quantity: number;
}

const products = reactive<ProductsProps[]>(
  [
    {
      id: 1,
      photo: "img/big-mac.png",
      name: "Big Mac",
      price: 5.99,
      active: false,
      quantity: 1
    },
    {
      id: 2,
      photo: "/img/mc-chicken.png",
      name: "Mc Chicken",
      price: 4.99,
      active: false,
      quantity: 1
    },
    {
      id: 3,
      photo: "img/double-cb.png",
      name: "Double Cheese Burger",
      price: 2.98,
      active: false,
      quantity: 1
    },
    {
      id: 4,
      photo: "img/fries.png",
      name: "Fries",
      price: 2.99,
      active: false,
      quantity: 1
    },
    {
      id: 5,
      photo: "img/nuggets.png",
      name: "Mc Nuggets",
      price: 3.49,
      active: false,
      quantity: 1
    },
    {
      id: 6,
      photo: "img/salad.png",
      name: "Salad",
      price: 2.79,
      active: false,
      quantity: 1
    },
    {
      id: 7,
      photo: "img/cola.png",
      name: "Coke",
      price: 1.99,
      active: false,
      quantity: 1
    },
    {
      id: 8,
      photo: "img/lipton.png",
      name: "Ice Tea",
      price: 1.98,
      active: false,
      quantity: 1
    },
    {
      id: 9,
      photo: "img/water.png",
      name: "Water",
      price: 1.49,
      active: false,
      quantity: 1
    }
  ]
)


function totalValue(){

  var total: number = 0;

  products.forEach(function(item: any){
    if(item.active){
    total = total + (item.price * item.quantity);
    }
  });
  return total.toFixed(2);
}

</script>

<template>
  <section class="container_items">

    <div class="products">
      <h1>Fast Food</h1>
      <h3>Pick your items</h3>
      <div v-for="product in products" :key="product.id" class="product" @click="product.active = !product.active"
        :class="{ selected: product.active }">
        <img :src="product.photo" alt="food image" class="image">
        <span>{{ product.name }}</span>
        <span>${{ product.price }}</span>
        <div class="quantity-area" v-if="product.active">
          <button @click.stop="product.quantity--" :disabled="product.quantity <= 1">-</button>
          <span class="quantity">{{ product.quantity }}</span>
          <button @click.stop="product.quantity++">+</button>
        </div>
      </div>
    </div>
    <div class="summary" v-if="Number(totalValue())>0">
      <strong>Order Details</strong>
      <table>
        <thead>
          <tr>
            <th>Item</th>
            <th>Total</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="product in products" :key="product.id">
            <td v-if="product.active">{{ product.quantity + 'x ' + product.name }}</td>
            <td v-if="product.active">{{ (product.quantity * product.price).toFixed(2) }}</td>
          </tr>

          <tr>
            <th>Total</th>
            <th>{{ totalValue() }}</th>
          </tr>
        </tbody>
      </table>

    </div>

  </section>
</template>

<style scoped>
.container_items {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  flex-wrap: wrap;
  padding: 20px;
  padding-top: 20px;
  font-family: Arial, Helvetica, sans-serif;

}

.selected {
  box-shadow: rgba(0, 0, 0, 0.15) 1.95px 1.95px 2.6px;
  border-radius: 10px;
  background-color: rgba(233, 29, 29, 0.486);
}

.quantity-area button {
  width: 16px;
  height: 16px;
  margin-top: 5px;
  display: inline-flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}

.image {
  width: 80px;
}

.container_items h1,
h3 {
  text-align: center;
  width: 100%;
}

.products {
  display: flex;
  flex-wrap: wrap;
  padding: 30px;
  max-width: 500px;
  min-width: 300px;
  justify-content: center;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
}

.product {

  display: flex;
  align-items: center;
  margin: 6px;
  flex: 0 0 calc(33.333% - 24px);
  cursor: pointer;
  width: 200px;
  height: 150px;
  justify-content: center;
  flex-direction: column;
}

.product span {
  font-size: 14px;
  line-height: 15px;
  text-align: center;
}

.summary {
  background-color: rgb(245, 245, 245);
  padding: 20px;
  color: #000;
  min-height: 200px;
  min-width: 200px;
  text-align: center;
  box-shadow: rgba(0, 0, 0, 0.15) 1.95px 1.95px 2.6px;
  border-radius: 5px;
}

.summary table {
  width: 100%;
  padding-top: 12px;
  font-size: 14px;
  margin: auto;
}

.summary table tbody tr:last-of-type th {
  border-top: 1px solid black;
  padding-top: 4px;
}
</style>