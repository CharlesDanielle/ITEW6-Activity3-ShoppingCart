<template>
    <h4>NOTE: We have the list of products and their price, click the [Add to Cart] button to add it on your cart table.</h4>
      
    <div>
      <h1>Shopping Cart</h1>
      <table>
        <!-- Cart Table Header -->
        <thead>
          <tr>
            <th>Product</th>
            <th>Price</th>
            <th>Quantity</th>
            <th>Total</th>
            <th>Action</th>
          </tr>
        </thead>
        <!-- Cart Table Body -->
        <tbody>
          <tr v-for="(item, index) in cart" :key="index">
            <td>{{ item.name }}</td>
            <td>{{ item.price }}</td>
            <td>
              <input type="number" v-model="item.quantity" min="1" @input="updateQuantity(index)">
            </td>
            <td>{{ item.total }}</td>
            <td>
              <button @click="removeItem(index)">Remove</button>
            </td>
          </tr>
        </tbody>
      </table>
  
      <hr> <!-- Horizontal line -->
  
      <h2>Total Price: Php {{ totalPrice }}</h2>

      <hr>

      <h1>Products</h1>
      <table>
        <!-- Products Table Header -->
        <thead>
          <tr>
            <th>Product</th>
            <th>Price</th>
            <th>Action</th>
          </tr>
        </thead>
        <!-- Products Table Body -->
        <tbody>
          <tr v-for="(product, index) in products" :key="index">
            <td>{{ product.name }}</td>
            <td>{{ product.price }}</td>
            <td>
              <button @click="addItem(product)">Add to Cart</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        products: [
          { name: 'Rice (kl)', price: 68 },
          { name: 'Fish (kl)', price: 200 },
          { name: 'Pork (kl)', price: 300 },
          { name: 'Beef (kl)', price: 350 },
          { name: 'Chicken (kl)', price: 230 },
          { name: 'Hotdog (pack)', price: 120 },
          { name: 'Footlong (pack)', price: 160 },
          { name: 'Fries (pack)', price: 125 },
          { name: 'Kikiam (pack)', price: 40 },
          { name: 'Fishball (pack)', price: 60 },
        ],
        cart: [],
      };
    },
    computed: {
      totalPrice() {
        return this.cart.reduce((acc, item) => acc + item.total, 0);
      },
    },
    methods: {
      addItem(product) {
        const existingItem = this.cart.find(item => item.name === product.name);
        if (existingItem) {
          existingItem.quantity++;
          existingItem.total = existingItem.price * existingItem.quantity;
        } else {
          this.cart.push({
            name: product.name,
            price: product.price,
            quantity: 1,
            total: product.price,
          });
        }
      },
      removeItem(index) {
        this.cart.splice(index, 1);
      },
      updateQuantity(index) {
        const item = this.cart[index];
        item.total = item.price * item.quantity;
      },
    },
  };
  </script>
  
  <style scoped>
  table {
    width: 100%;
    border-collapse: collapse;
  }
  
  th, td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: left;
  }
  
  th {
    background-color: #f2f2f2;
  }
  
  button {
    padding: 5px 10px;
    cursor: pointer;
  }
  h4{
    text-align: left;
  }
  </style>
  