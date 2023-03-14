<template>
  <div class="black-bg" v-if="modalOpenStatus">
    <div class="white-bg">
      <img :src="rooms[clickedID].image" class="room-img" alt="">
      <h4>{{ rooms[clickedID].title }}</h4>
      <p>{{ rooms[clickedID].content }}</p>
      <input v-model="month">
<!--      <input @input="month = $event.target.value">-->
      개월
      <p>{{month}}개월 선택 {{ month * rooms[clickedID].price }} 원</p>
      <DiscountBill></DiscountBill>
      <button @click="closeModal">닫기</button>
    </div>
  </div>
</template>

<script>
import DiscountBill from "@/DiscountBill.vue";
export default {
  name: "ModalMoreInformation",
  components: {
    DiscountBill,
  },
  props: {
    rooms: Array,
    modalOpenStatus: Boolean,
    clickedID: Number,
  },
  methods: {
    closeModal() {
      this.$emit('closeModal');
    }
  },
  data () {
    return{
      month: 1,
    }
  },
  watch: {
    month(inputData) {
      if(isNaN(inputData) == true) {
        alert('숫자만 입력 가능합니다.');
      }
      if(inputData > 12) {
        alert('최대 12개월까지 선택 가능합니다.');
        this.month = 12;
      }
    }
  }
}
</script>

<style>
/*modal*/
.black-bg {
  width: 100%; height:100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
}
</style>