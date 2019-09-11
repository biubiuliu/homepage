<template>
  <div class="card_body">
    <div class="bar_card" v-for="(item,index) in cardData" :key="index" v-on:click="handCardRouter(item)" >
      <div class="bar_card_box">
        <img class="bar_card_img" :src="item.img" alt="图片不存在">
        <div class="bar_card_title">{{item.title}}</div>
        <div class="bar_card_subhead">{{item.subhead}}</div>
        <p class="bar_card_content">{{item.content}}</p>
        <br/>
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
  flex-wrap:wrap ;
  cursor: pointer;
  font-size: 12px;

}
.bar_card_box{
  margin: 10px;
  background: white;
  padding: 5px;
  height: 90%;
  transition:box-shadow .5s;
}
.bar_card_box:hover{
   box-shadow:-4px 8px 20px #333333;

}
.bar_card_img{
  width: 100%;
  height: 40%;

}
.bar_card_title{
  margin-top: 5px;
  font-size: 200% ;
  color: #6b82ac
}
.bar_card_subhead{
  margin-top: 5px;
  font-size: 150% ;
  color: #80818379
}
.bar_card_content{
  padding: 0 5px;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 3;
  overflow: hidden;
}
.bar_card{
  width: 20%;

}
@media (max-width: 900px) {
  .bar_card_title{
    font-size: 100%;
    color: #6b82ac
  }
  .bar_card_subhead{
    margin-top: 5px;
    font-size: 50% ;
    color: #80818379
  }
  .bar_card{
    width: 33%;
  }
}
@media (min-width: 900px) and (max-width: 1500px) {
  .bar_card_title{
    font-size: 125%;
    color: #6b82ac
  }
  .bar_card_subhead{
    margin-top: 5px;
    font-size: 75% ;
    color: #80818379
  }
  .bar_card{
    width: 20%;
  }
  .bar_card_box{
    margin: 10px;
    background: white;
    padding: 5px;
    height: 80%;
  }
}
@media (min-width: 1500px) and (max-width: 1900px) {
  .bar_card_title{
    font-size: 150%;
    color: #6b82ac
  }
  .bar_card_subhead{
    margin-top: 5px;
    font-size: 100% ;
    color: #80818379
  }
  .bar_card{
    width: 20%;
  }
}
</style>
