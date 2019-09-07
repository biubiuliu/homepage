<template>
  <div class="hello">
      <header>
        <ul id="searchEnginPic" class="searchEnginPic">
            <li class="active">
                <a href="https://www.google.com.hk/" target="_blank"><img src="../assets/google.png" alt="google"></a>
            </li>
            <li>
                <a href="https://www.baidu.com/" target="_blank"><img src="../assets/baidu.gif" alt="百度一下"></a>
            </li>
        </ul>
        <form action="" id="searchBar" class="searchBar">
            <ul id="searchEnginLogo"  class="searchEnginLogo">
                <li class="active">
                    <img @click="switchSearchEngin" src="../assets/google.svg" alt="google">
                </li>
                <li>
                    <img @click="switchSearchEngin" src="../assets/baidu.svg" alt="baidu">
                </li>
            </ul>
            <input type="text" id="inputBar" placeholder = '点击左边图标切换搜索引擎'>
            <button id="searchBtn" class="searchBtn"></button>
            <button id="searchBtn" class="searchBtn"></button>
        </form>
    </header>
    <div id="main">
      <bar-card @handCardRouter='handCardRouter' :cardData='cardData'></bar-card>
    </div>
  </div>
</template>

<script>
import BarCard from './card/barCard'
export default {
  components: {
    BarCard
  },
  name: 'home',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      ifSwitch: false,
      ifInputting: false,
      cardData: [
        {
          title: '百度',
          url: 'baidu',
          img: 'https://cdn.jsdelivr.net/npm/@bootcss/www.bootcss.com@0.0.3/dist/img/babeljs.png'
        },
        {
          title: '谷歌',
          url: 'google',
          img: 'https://cdn.jsdelivr.net/npm/@bootcss/www.bootcss.com@0.0.3/dist/img/jqueryapi.png'
        },
        {
          title: '谷歌',
          url: 'google',
          img: 'https://cdn.jsdelivr.net/npm/@bootcss/www.bootcss.com@0.0.3/dist/img/jqueryapi.png'
        },
        {
          title: '谷歌',
          url: 'google',
          img: 'https://cdn.jsdelivr.net/npm/@bootcss/www.bootcss.com@0.0.3/dist/img/jqueryapi.png'
        },
        {
          title: '斗鱼',
          url: '斗鱼',
          img: 'https://cdn.jsdelivr.net/npm/@bootcss/www.bootcss.com@0.0.3/dist/img/babeljs.png'
        }
      ]

    }
  },
  mounted () {
    this.listenToUser()
  },
  methods: {
    listenToUser () {
      // ifInputting作为一个开关
      this.ifInputting = false
      let inputBar = document.getElementById('inputBar')
      let searchBtn = document.querySelector('.searchBtn')
      inputBar.addEventListener('focus', function (e) {
        this.ifInputting = true
        e.target.placeholder = ''
      })
      inputBar.addEventListener('focusout', function (e) {
        this.ifInputting = false
        let searchEnginLogo = document.getElementById('searchEnginLogo')
        let engin = searchEnginLogo.getAttribute('data-engin')
        e.target.placeholder = '点击左边图标切换搜索引擎'
        switch (engin) {
          case 'baidu':
            e.target.placeholder = '众里寻他千百度，蓦然回首，那人却在灯火阑珊处'
            break
          case 'google':
            e.target.placeholder = '昨夜西风凋碧树，独上高楼，望尽天涯路'
            break
        }
      })
      searchBtn.onclick = function (e) {
        e.preventDefault()
        let searchContent = inputBar.value
        // 判断是什么搜索引擎
        let searchEnginLogo = document.getElementById('searchEnginLogo')
        let engin = searchEnginLogo.getAttribute('data-engin')

        switch (engin) {
          case 'baidu':
            window.open('https://www.baidu.com/s?wd=' + searchContent, '_blank')
            break
          case 'google':
            window.open('https://www.google.com.hk/search?q=' + searchContent, '_blank')
            break
        }
      }
    },
    switchSearchEngin () {
    // 搜索引擎默认是google
      let searchEnginLogo = document.getElementById('searchEnginLogo')
      let googleLogo = document.querySelector('#searchEnginLogo li:nth-child(1)')
      let baiduLogo = document.querySelector('#searchEnginLogo li:nth-child(2)')
      let googlePic = document.querySelector('#searchEnginPic li:nth-child(1)')
      let baiduPic = document.querySelector('#searchEnginPic li:nth-child(2)')
      let inputBar = document.getElementById('inputBar')
      searchEnginLogo.setAttribute('data-engin', 'google')
      searchEnginLogo.onclick = () => {
        if (!this.ifSwitch) {
          // google --> baidu
          googleLogo.classList.remove('active')
          baiduLogo.classList.add('active')
          googlePic.classList.remove('active')
          baiduPic.classList.add('active')
          searchEnginLogo.setAttribute('data-engin', 'baidu')
          inputBar.placeholder = '众里寻他千百度，蓦然回首，那人却在灯火阑珊处'
        } else {
          // baidu --> google
          baiduLogo.classList.remove('active')
          googleLogo.classList.add('active')
          baiduPic.classList.remove('active')
          googlePic.classList.add('active')
          searchEnginLogo.setAttribute('data-engin', 'google')
          inputBar.placeholder = '昨夜西风凋碧树，独上高楼，望尽天涯路'
        }
        this.ifSwitch = !this.ifSwitch
        console.log(this.ifSwitch)
      }
    },
    handCardRouter (item) {
      console.log(item)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
*{margin: 0;padding:0;}
ul{list-style: none;}
.clearfix::after{
    content: '';
    display: block;
    clear: both;
}
/* header */
header{
    width: 720px;
    height: 44px;
    margin: 100px auto 50px;
}
header .searchEnginPic{
    float: left;
    width: 120px;
    height: 44px;
}
header .searchEnginPic li{
    display: none;
}
header .searchEnginPic li.active{
    display: inline-block;
}
header .searchEnginPic li:nth-child(1) img{
    width: 120px;
    padding: 2.5px 0;
}
header .searchEnginPic li:nth-child(2) img{
    width: 120px;
    height: 44px;
}

header .searchBar{
    float: right;
    width: 580px;
    height: 44px;
    border-radius: 24px;
    position: relative;
    background: #fff;
}
header .searchBar:hover{
    box-shadow: 0 1px 6px 0 rgba(32,33,36,0.28);
    border-color: rgba(223,225,229,0);
}
header .searchBar .searchEnginLogo{
    position: absolute;
    left: 10px;
    width: 24px;
    height: 44px;
    cursor: pointer;
}
header .searchBar .searchEnginLogo li{
    display: none;
}
header .searchBar .searchEnginLogo li.active{
    display: inline-block;
}
.searchBar .searchEnginLogo li img{
    width: 24px;
    height: 24px;
    padding: 10px 0;
}
.searchBar input{
    position: absolute;
    left: 46px;
    top: 10%;
    width: 505px;
    height: 80%;
    border: none;
    outline: none;
}
.searchBar .searchBtn{
    position: absolute;
    right: 6px;
    top: 7px;
    width: 30px;
    height: 30px;
    background: url(../assets/search-btn.png) center center no-repeat;
    cursor: pointer;
    border: none;
    outline: none;
}
#main{
  border: 1px solid red;
  width: 80%;
  height: 500px;
  margin: 0 auto;
  padding: 10px
}
</style>
