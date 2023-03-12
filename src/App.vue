<template>
  <div class="black-bg" v-if="modalOpenStatus">
    <div class="white-bg">
      <img :src="rooms[clickedID].image" class="room-img" alt="">
      <h4>{{ rooms[clickedID].title }}</h4>
      <p>{{ rooms[clickedID].content }}</p>
      <p>{{ rooms[clickedID].price }} 원</p>
      <button @click="modalOpenStatus = false">닫기</button>
    </div>
  </div>

  <div>
    <div class="menu">
      <a v-for="menu in headerMenus" :key="menu">{{ menu }}</a>
    </div>
  </div>
  <div v-for="(product,i) in products" :key="product" class="roomProducts">
    <img :src="rooms[i].image" class="room-img"
         @click="modalOpenStatus = true; clickedID= i;" alt="">
    <h4>{{ rooms[i].title }} 원룸</h4>
    <p>{{ rooms[i].price }} 원</p>
    <button @click="increaseReport(i)">허위매물신고</button> <span>신고 수:
    {{reportCount[i]}}</span>
  </div>
</template>

<script>
import roomData from './assets/oneroom.js';
export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      clickedID: 0,
      rooms: roomData,
      products: ['역삼동','천호동','마포구'],
      price: [10,20,30],
      headerMenus: ['Home','Products','About'],
      modalOpenStatus: false,
    }
  },
  computed: {
    reportCount() {
      return new Array(this.products.length).fill(0);
    }
  },
  methods: {
    increaseReport(index) {
      this.reportCount[index] += 1;
      console.log(this.reportCount)
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

.menu {
  background : darkslateblue;
  padding : 15px;
  border-radius : 5px;
}
.menu a {
  color : white;
  padding : 10px;
}
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
