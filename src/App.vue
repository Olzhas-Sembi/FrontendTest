<script setup lang="ts">
import { ref } from 'vue';

interface Order {
  itemName: string;
  address: string;
  status: 'В обработке' | 'В пути' | 'Доставлено';
}

const orders = ref<Order[]>([
  { itemName: 'Пицца', address: 'ул. Ленина 10', status: 'В обработке' },
  { itemName: 'Книга', address: 'пр. Мира 5', status: 'Доставлено' }
]);

const newOrder = ref<Order>({ itemName: '', address: '', status: 'В обработке' });

const addOrder = () => {
  if (newOrder.value.itemName && newOrder.value.address) {
    orders.value.push({ ...newOrder.value });
    newOrder.value = { itemName: '', address: '', status: 'В обработке' };
  }
};
</script>

<template>
  <div class="container">
    <h1>Список заказов</h1>
    <table>
      <tr>
        <th>Товар</th>
        <th>Адрес</th>
        <th>Статус</th>
      </tr>
      <tr v-for="(order, index) in orders" :key="index">
        <td>{{ order.itemName }}</td>
        <td>{{ order.address }}</td>
        <td>{{ order.status }}</td>
      </tr>
    </table>

    <h2>Добавить заказ</h2>
    <form @submit.prevent="addOrder">
      <input v-model="newOrder.itemName" placeholder="Название товара" required />
      <input v-model="newOrder.address" placeholder="Адрес доставки" required />
      <select v-model="newOrder.status">
        <option>В обработке</option>
        <option>В пути</option>
        <option>Доставлено</option>
      </select>
      <button type="submit">Добавить заказ</button>
    </form>
  </div>
</template>


