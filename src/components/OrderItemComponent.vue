<template>
  <div class="order-item">
    <img :src="item.image" :alt="item.name">
    <div class="order-item-info">
      <span class="item-name">{{ item.name }}</span>
      <span class="item-price">￥{{ item.price }}</span>
    </div>
  </div>
</template>

<script setup lang="ts">

defineProps<{
  item: Item;
}>();
</script>


<style scoped>
.order-item {
  height: 100px;
  width: 100%;
  display: flex;
  flex-direction: row;
  padding: 10px;
  box-sizing: border-box;
  border-radius: 5px;
  margin-bottom: 2px;
  background-color: #fff;
  box-shadow: 1px 1px 1px 1px #ccc;
  cursor: pointer;

  .order-item-info {
    display: flex;
    flex-direction: column;
    margin-left: 20px;
    font-size: 14px;
    align-items: center;
    justify-content: center;

    .item-name {
      font-size: 18px;
      font-weight: bold;
      margin-bottom: 10px;
    }
  }
}
</style>