<template>
  <h2 class="title">在线订单系统</h2>
  <div class="order-root">
    <div class="left">
      <div class="order-list">
        <OrderItemComponent
            v-for="item in items"
            :key="item.id"
            :item="item"
            @click="selectItem(item)"
        ></OrderItemComponent>
      </div>
    </div>
    <div class="right">
      <div class="right-top">
        <OrderItemComponent
            v-for="item in selectedItem"
            :key="item.id"
            :item="item"
        ></OrderItemComponent>
      </div>
      <div class="right-bottom">
        <div class="amount">总计: {{ totalAmount }}</div>
        <div class="quantity">数量: {{ quantity }}</div>
        <el-button class="order-button" plain @click="clearItem">清空</el-button>
        <el-button class="order-button" plain>下单</el-button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">

import {computed, reactive, ref} from "vue";
import OrderItemComponent from "./OrderItemComponent.vue";
import {ElMessage} from "element-plus";

const items = reactive([
  {
    id: 1,
    name: 'IPhone 16',
    price: 9999.99,
    image: '/images/iphone16.png'
  },
  {
    id: 2,
    name: 'IPhone 15',
    price: 8999.99,
    image: '/images/iphone15.png'
  },
  {
    id: 2,
    name: 'IPhone 14',
    price: 7999.99,
    image: '/images/iphone14.png'
  }
])
const selectedItem = ref<Item[]>([]);
const amount = ref(0);
const quantity = ref(0);

const selectItem = (item: Item) => {
  amount.value += item.price;
  quantity.value += 1;
  selectedItem.value.push(item)
}

const totalAmount = computed(() => {
  return amount.value.toFixed(2);
})

const clearItem = () => {
  selectedItem.value = [];
  amount.value = 0;
  quantity.value = 0;

  ElMessage({
    message: '清空成功',
    type: 'success',
    plain: true,
  })
}

// const selectedRemove = (item: Item) => {
//   amount.value -= item.price;
//   quantity.value -= 1;
//   const index = selectedItem.value.filter(user => user.id !== item.id)
//   if (index !== -1) {
//     selectedItem.value.splice(index, 1);
//   }
// }

</script>

<style scoped>
.title {
  color: #eee;
  font-size: 40px;
  font-weight: bold;
  text-align: center;
  margin-bottom: 20px;
}

.order-root {
  height: 600px;
  width: 600px;
  box-shadow: 1px 1px 5px 1px #ccc;
  border-radius: 5px;
  display: flex;
  flex-direction: row;
  background-color: #fff;
}

.left {
  height: 100%;
  width: 50%;
  border-right: 1px solid #ccc;
  padding: 5px 0;

  .order-list {
    height: 100%;
    width: 100%;
  }
}

.right {
  height: 100%;
  width: 50%;
  display: flex;
  flex-direction: column;
  padding: 10px;
  box-sizing: border-box;

  .right-top {
    height: 80%;
    width: 100%;
    border-bottom: 1px solid #ccc;
    overflow: auto;
  }

  .right-bottom {
    display: flex;
    flex-direction: column;
    padding: 10px;

    .order-button {
      align-self: flex-end;
    }
  }
}
</style>