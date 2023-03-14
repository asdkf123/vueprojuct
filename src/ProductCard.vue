<template>
  <div class="roomProducts">
    <img :src="rooms.image" class="room-img" alt=""
         @click="openModal">
    <h4>{{ rooms.title }} 원룸</h4>
    <p>{{ rooms.price }} 원</p>
    <button @click="$emit('increaseReport')">허위매물신고</button>
    <span>신고 수:
    {{reportCount}}</span>
  </div>
</template>

<script>
export default {
  name: "ProductCard",
  props: {
    rooms: Object,
    reportCount: Array,
    // modalOpenStatus: Boolean,
    clickedID: Number,
  },
  methods: {
    openModal() {
      this.$emit('openModal', this.rooms.id);
    }
  }
}
</script>

<style>
.roomProducts {
  display : inline-block;
  width : 380px;
  margin : 10px;
  padding : 10px;
  border : 1px solid #ccc;
  border-radius : 5px;
}
.room-img {
  width : 300px;
  height : 200px;
  border-radius : 5px;
}
</style>