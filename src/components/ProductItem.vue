<script>
import itemImg from '@/assets/item.png'

export default {
  props: ['item', 'deletedItem'],

  data() {
    return {
      itemImg: itemImg,
    }
  },
  methods: {}
}
</script>

<template>
  <div class="item" :class="{ deleted: deletedItem }">
    <img :src="itemImg" alt="">
    <div class="item-title">{{ item.title }}</div>
    <div>{{ item.body }}</div>
    <button v-show="!deletedItem" class="item-btn" @click="$emit('remove', item)">
      <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-x-circle"
           viewBox="0 0 16 16">
        <path d="M8 15A7 7 0 1 1 8 1a7 7 0 0 1 0 14zm0 1A8 8 0 1 0 8 0a8 8 0 0 0 0 16z"/>
        <path
            d="M4.646 4.646a.5.5 0 0 1 .708 0L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 0 1 0-.708z"/>
      </svg>
    </button>
  </div>
</template>

<style scoped>

.item {
  background: blue;
  color: white;
  padding: 20px;
  position: relative;
}

.item-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  position: absolute;
  top: 15px;
  right: 15px;
  background: blue;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  color: white;
  border: none;
  cursor: pointer;
  transform: scale(1.5);
  transition: all 0.3s ease;
}

.item-btn:hover{
  color: red;
}

.deleted {
  opacity: 0.5;
  text-decoration: line-through;
}

.item-title{
  margin-top: 20px;
}

</style>