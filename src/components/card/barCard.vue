<template>
  <div class="card_body">
    <div v-for="(item,index) in cardData" :key="index" class="bar_card" @click="handCardRouter(item)">
      <div :style="editBtn" class="bar_card_box">
        <img v-lazy="item.img" :style="{'background':colorList[index] }" class="bar_card_img" alt="图片不存在">
        <div class="bar_card_title">{{ item.title }}</div>
        <div class="bar_card_subhead">{{ item.subhead }}</div>
        <p class="bar_card_content">{{ item.content }}</p>
        <br>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'Barcard',
  props: {
    cardData: {
      type: Array,
      default: () => []
    },
    editBtn: {
      type: Object,
      default: () => { }
    }
  },
  data() {
    return {
      colorArr: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f'],
      colorList: []
    }
  },
  created() {
    for (let i = 0; i < this.cardData.length; i++) {
      this.colorList.push(this.method1())
    }
    // console.log(this.colorList)
  },
  methods: {
    handCardRouter(item) {
      this.$emit('handCardRouter', item)
    },
    random(min, max) {
      if (isNaN(min) || isNaN(max)) {
        return null
      }
      if (min > max) {
        min ^= max
        max ^= min
        min ^= max
      }
      return (Math.random() * (max - min) | 0) + min
    },
    method1() {
      var color = '#'
      for (var i = 0; i < 6; i++) {
        color += this.colorArr[this.random(0, 16)]
      }
      // console.log(color)
      return color
    }
  }
}
</script>
<style scope>
.card_body {
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
  cursor: pointer;
  font-size: 12px;
}
.bar_card_box {
  margin: 10px;
  background: white;
  padding: 5px;
  height: 90%;
  transition: box-shadow 0.5s;
}
.bar_card_box:hover {
  box-shadow: -4px 8px 20px #333333;
}
.bar_card_img {
  width: 100%;
  height: 40%;
  background: #6b82ac;
}
.bar_card_title {
  margin-top: 5px;
  font-size: 200%;
  color: #6b82ac;
}
.bar_card_subhead {
  margin-top: 5px;
  font-size: 150%;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 1;
  overflow: hidden;
  color: #80818379;
}
.bar_card_content {
  padding: 0 5px;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 3;
  overflow: hidden;
}
.bar_card {
  width: 20%;
}
@media (max-width: 900px) {
  .bar_card_title {
    font-size: 100%;
    color: #6b82ac;
  }
  .bar_card_subhead {
    margin-top: 5px;
    font-size: 50%;
    color: #80818379;
  }
  .bar_card {
    width: 33%;
  }
}
@media (min-width: 900px) and (max-width: 1500px) {
  .bar_card_title {
    font-size: 125%;
    color: #6b82ac;
  }
  .bar_card_subhead {
    margin-top: 5px;
    font-size: 75%;
    color: #80818379;
  }
  .bar_card {
    width: 20%;
  }
  .bar_card_box {
    margin: 10px;
    background: white;
    padding: 5px;
    height: 80%;
  }
}
@media (min-width: 1500px) and (max-width: 1900px) {
  .bar_card_title {
    font-size: 150%;
    color: #6b82ac;
  }
  .bar_card_subhead {
    margin-top: 5px;
    font-size: 100%;
    color: #80818379;
  }
  .bar_card {
    width: 20%;
  }
}
</style>
