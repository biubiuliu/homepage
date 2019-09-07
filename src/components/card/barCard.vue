<template>
  <div class="card_body">
    <div class="bar_card" v-for="(item,index) in cardData" :key="index" v-on:click="handCardRouter(item)" >
      <div class="bar_card_box">
        <img class="bar_card_img" :src="item.img" alt="图片不存在">
        <div class="bar_card_title">{{item.title}}</div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'barcard',
  props: {
    cardData: Array
  },
  data () {
    return {

    }
  },
  methods: {
    handCardRouter (item) {
      this.$emit('handCardRouter', item)
    }
  }
}
</script>
<style scope>
.card_body{
  display: flex;
  justify-content: flex-start;
  cursor: pointer;
  font-size: 12px;

}
.bar_card_box{
  margin: 10px;
  background: white;
}
.bar_card_img{
  width: 100%
}
.bar_card_title{
  font-size: 200%;
  color: #475164
}
.bar_card{
  width: 40%
}
</style>
