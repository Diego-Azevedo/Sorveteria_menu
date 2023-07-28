<template>
  <div class="app">
    <div class="menu">
      <h1>Cardápio IslandRoll</h1>
      <div v-for="item in menu" :key="item.id" class="menu-item">
        <span>{{ item.name }}</span>
        <div class="price-container">
          <button @click="decrement(item)">-</button>
          <span>{{ item.quantity }}</span>
          <button @click="increment(item)">+</button>
          <span>{{ formatPrice(item.price) }}</span>
        </div>
      </div>
    </div>
    <div class="footer">
      <div v-for="item in selectedItems" :key="item.id" class="selected-item">
        <span>{{ item.name }}</span>
        <span>{{ item.quantity }}</span>
        <span>{{ formatPrice(item.price) }}</span>
      </div>
      <div class="total">
        <span>Total:</span>
        <span>{{ formatPrice(totalPrice) }}</span>
      </div>
      <button @click="confirmOrder">Confirmar Compra</button>
      <button @click="cancelOrder">Cancelar Compra</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      menu: [
        { id: 1, name: 'Sorvete de Baunilha', price: 5, quantity: 0 },
        { id: 2, name: 'Sorvete de Chocolate', price: 5, quantity: 0 },
        { id: 3, name: 'Sorvete de Morango', price: 5, quantity: 0 },
        // Adicione outros sabores de sorvete aqui
      ],
      selectedItems: [],
    };
  },
  computed: {
    totalPrice() {
      return this.selectedItems.reduce((total, item) => total + item.price * item.quantity, 0);
    },
  },
  methods: {
    increment(item) {
      item.quantity++;
      this.addToSelectedItems(item);
    },
    decrement(item) {
      if (item.quantity > 0) {
        item.quantity--;
        this.removeFromSelectedItems(item);
      }
    },
    addToSelectedItems(item) {
      if (!this.selectedItems.includes(item)) {
        this.selectedItems.push(item);
      }
    },
    removeFromSelectedItems(item) {
      const index = this.selectedItems.indexOf(item);
      if (index !== -1) {
        this.selectedItems.splice(index, 1);
      }
    },
    formatPrice(price) {
      return `R$ ${price.toFixed(2)}`;
    },
    confirmOrder() {
      // Implemente a lógica para confirmar a compra
      console.log('Compra confirmada:', this.selectedItems);
      this.resetMenu();
    },
    cancelOrder() {
      // Implemente a lógica para cancelar a compra
      console.log('Compra cancelada');
      this.resetMenu();
    },
    resetMenu() {
      this.menu.forEach((item) => (item.quantity = 0));
      this.selectedItems = [];
    },
  },
};
</script>

<style>
.app {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100vh;
  font-family: Arial, sans-serif;
  background-color: rgb(207, 207, 43);
}

.menu {
  padding: 20px;
}

.menu-item {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
}

.price-container {
  display: flex;
  align-items: center;
}

.footer {
  background-color: #f0f0f0;
  padding: 20px;
  position: fixed;
  bottom: 0;
  width: 95%;
}

.selected-item {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
}

.total {
  display: flex;
  justify-content: space-between;
  font-weight: bold;
}

h1 {
  text-align: center;
}
</style>
