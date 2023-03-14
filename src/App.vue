<template>
  <!--  moreInfo-modal-->
  <div class="start" :class="{end : modalOpenStatus}" >
    <ModalMoreInformation
        :rooms="rooms"
        :modalOpenStatus="modalOpenStatus"
        :clickedID="clickedID"
        @closeModal="modalOpenStatus = false"
    />
  </div>

<!--  header-->
  <div>
    <div class="menu">
      <a v-for="menu in headerMenus" :key="menu">{{ menu }}</a>
    </div>
  </div>

<!--  discount-->
  <DiscountBill />

<!--  product-->
  <ProductCard :rooms="rooms[i]"
    @openModal="modalOpenStatus = true; clickedID= $event"
    v-for="(room, i) in rooms" :key="i"
  />
<!--    @increaseReport="increaseReport(i)"-->
<!--    :reportCount="reportCount"-->
<!--      :modalOpenStatus="modalOpenStatus"-->


</template>

<script>
import roomData from './assets/oneroom.js';
import DiscountBill from "@/DiscountBill.vue";
import ModalMoreInformation from "@/ModalMoreInformation.vue";
import ProductCard from "@/ProductCard.vue";
export default {
  name: 'App',
  components: {
    ModalMoreInformation,
    DiscountBill,
    ProductCard,
  },
  data() {
    return {
      clickedID: 0,
      rooms: roomData,
      headerMenus: ['Home','Products','About'],
      modalOpenStatus: false,
    }
  },
  computed: {
    reportCount() {
      return new Array(this.rooms.length).fill(0);
    }
  },
  methods: {
    increaseReport(index) {
      this.reportCount[index] += 1;
      console.log(this.reportCount);
    },
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

body {
  margin : 0;
}
div {
  box-sizing: border-box;
}

.start {
  opacity: 0;
  transition: all 1s;
}

.end {
  opacity: 1;
}

.menu {
  background : darkslateblue;
  padding : 15px;
  border-radius : 5px;
}
.menu a {
  color : white;
  padding : 10px;
}

</style>
