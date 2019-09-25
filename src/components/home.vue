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
        </form>
    </header>
    <div id="main">
      <button  @click="editBtn">编辑</button>
      <button  @click="successBtn">完成</button>
      <bar-card @handCardRouter='handCardRouter' :editBtn='editBtnData' :cardData='cardData'></bar-card>
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
      editBtnData: {
        position: 'relative',
        transform: ' rotate(0deg)',
        left: '-2px',
        top: '-1px'
      },
      leftArr: [-1, 0, 1, 2],
      topArr: [-1, 0, 1, 2],
      rotateArr: [-1, 0, 1],
      setIntervalData: '',
      cardData: [
        {
          title: 'Node.js',
          subhead: '中文文档',
          url: 'https://www.nodeapp.cn/',
          img: '../../../static/img/nodejs.png',
          content: 'Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。Node.js 使用了一个事件驱动、非阻塞式 I/O 的模型，使其轻量又高效。'
        },
        {
          title: 'Vue.js',
          subhead: '中文文档',
          url: 'https://vuejs.bootcss.com/',
          img: '../../../static/img/vuejs.png',
          content: 'Vue.js - 是一套构建用户界面的渐进式框架。'
        },
        {
          title: 'React.js',
          subhead: '中文手册',
          url: 'https://www.reactjscn.com/',
          img: '../../../static/img/react.png',
          content: 'React 起源于 Facebook 的内部项目，是一个用于构建用户界面的 JavaScript 库。'
        },
        {
          title: 'ESLint',
          subhead: 'JavaScript 代码检查工具',
          url: 'https://cn.eslint.org/',
          img: '../../../static/img/eslint.png',
          content: 'ESLint 是一个插件化并且可配置的 JavaScript 语法规则和代码风格的检查工具。ESLint 能够帮你轻松写出高质量的 JavaScript 代码。'
        },
        {
          title: 'TypeScript',
          subhead: '用于构建用户界面的 JavaScript 框架',
          url: 'https://typescript.bootcss.com',
          img: '../../../static/img/typescript.png',
          content: 'TypeScript 是由微软开源的编程语言。它是 JavaScript 的一个超集，而且本质上向这个语言添加了可选的静态类型和基于类的面向对象编程。'
        },
        {
          title: 'github',
          subhead: '分布式代码仓库',
          url: 'https://github.com/',
          img: '../../../static/img/github.jpg',
          content: 'gitHub是一个面向开源及私有软件项目的托管平台,因为只支持git 作为唯一的版本库格式进行托管,故名gitHub。'
        },
        {
          title: 'iview',
          subhead: 'iview-ui',
          url: 'https://www.iviewui.com/',
          img: '../../../static/img/iview.png',
          content: '一套基于 Vue.js 的高质量UI 组件库'
        },
        {
          title: 'element',
          subhead: 'element-ui',
          url: 'https://element.eleme.cn/#/zh-CN',
          img: '../../../static/img/element-ui.png',
          content: 'Element，一套为开发者、设计师和产品经理准备的基于 Vue 2.0 的桌面端组件库'
        },
        {
          title: 'jQuery API',
          subhead: '中文手册',
          url: 'https://www.jquery123.com/',
          img: '../../../static/img/jqueryapi.png',
          content: '根据最新的 jQuery 1.11.x 和 2.1.x 版本翻译的 jQuery API 中文文档/手册。'
        },
        {
          title: 'Next.js',
          subhead: '中文文档',
          url: 'https://typescript.bootcss.com',
          img: '../../../static/img/nextjs.png',
          content: 'Next.js 是一个轻量级的 React 服务端渲染应用框架。'
        },
        {
          title: 'Webpack',
          subhead: '前端资源模块化管理和打包工具',
          url: 'https://www.webpackjs.com/',
          img: '../../../static/img/webpack.png',
          content: 'Webpack 是当下最热门的前端资源模块化管理和打包工具。它可以将许多松散的模块按照依赖和规则打包成符合生产环境部署的前端资源。'
        },
        {
          title: 'gulp.js',
          subhead: '基于流的自动化构建工具。',
          url: 'https://www.gulpjs.com.cn/',
          img: '../../../static/img/gulpjs.png',
          content: 'gulp.js - 基于流(stream)的自动化构建工具。Grunt 采用配置文件的方式执行任务，而 Gulp 一切都通过代码实现。'
        },
        {
          title: 'Grunt',
          subhead: '项目构建工具',
          url: 'https://www.gruntjs.net/',
          img: '../../../static/img/gruntjs.png',
          content: 'gulp.js - 基于流(stream)的自动化构建工具。Grunt 采用配置文件的方式执行任务，而 Gulp 一切都通过代码实现。'
        },
        {
          title: 'cnpm',
          subhead: '淘宝镜像',
          url: 'http://npm.taobao.org/',
          img: '../../../static/img/cnpm.jpg',
          content: '这是一个完整 npmjs.org 镜像，你可以用此代替官方版本(只读)，同步频率目前为 10分钟 一次以保证尽量与官方服务同步。'
        },
        {
          title: 'npm',
          subhead: 'npm 中文文档',
          url: 'https://www.npmjs.cn/',
          img: '../../../static/img/npm.png',
          content: 'npm 为你和你的团队打开了连接整个 JavaScript 天才世界的一扇大门。它是世界上最大的软件注册表，每星期大约有 30 亿次的下载量，包含超过 600000 个 包（package） （即，代码模块）。来自各大洲的开源软件开发者使用 npm 互相分享和借鉴。包的结构使您能够轻松跟踪依赖项和版本。'
        },
        {
          title: 'Babel',
          subhead: '是一个 JavaScript 编译器。',
          url: 'https://www.babeljs.cn/',
          img: '../../../static/img/babeljs.png',
          content: 'Babel 是一个 JavaScript 编译器。Babel 通过语法转换器支持最新版本的 JavaScript 语法。'
        },
        {
          title: 'yarn',
          subhead: 'yarn中文文档',
          url: 'https://yarn.bootcss.com/',
          img: '../../../static/img/yarn.png',
          content: 'Yarn 是一个快速、可靠、安全的依赖管理工具。是 NPM 的替代品。'
        },
        {
          title: 'Sass',
          subhead: 'CSS 扩展语言解析器',
          url: 'https://www.sasscss.com/',
          img: '../../../static/img/sass.png',
          content: 'Sass 是一个成熟、稳定、强大的 CSS 扩展语言解析器。'
        },
        {
          title: 'LESS',
          subhead: 'CSS 扩展语言解析器',
          url: 'https://www.bootcss.com/p/lesscss/',
          img: '../../../static/img/lesscss.png',
          content: 'LESS 为 CSS 赋予了动态语言的特性，如变量、继承、运算、函数。LESS 既可以在客户端上运行 (支持 IE 6+、Webkit、Firefox)，也可以借助 Node.js 或者 Rhino 在服务端运行。'
        },
        {
          title: 'Stylus',
          subhead: 'CSS 扩展语言解析器',
          url: 'https://stylus.bootcss.com/',
          img: '../../../static/img/stylus.png',
          content: 'Stylus - 富于表现力、健壮、功能丰富的 CSS 预处理语言。'
        },
        {
          title: '阿里iconfont',
          subhead: '阿里iconfont 字体库',
          url: 'https://www.iconfont.cn/home/index?spm=a313x.7781069.1998910419.2',
          img: '../../../static/img/aliiconfont.jpg',
          content: '用户可以自定义下载多种格式的icon，平台也可将图标转换为字体，便于前端工程师自由调整与调用。'
        },
        {
          title: 'Font Awesome',
          subhead: 'Awesome 字体库',
          url: 'https://www.bootcss.com/p/font-awesome/',
          img: '../../../static/img/font-awesome.png',
          content: 'Font Awesome 中包含的所有图标都是矢量的，也就可以任意缩放，避免了一个图标做多种尺寸的麻烦。CSS 对字体可以设置的样式也同样能够运用到这些图标上了。'
        },
        {
          title: 'Web Safe Colors',
          subhead: 'Web 安全色',
          url: 'https://www.bootcss.com/p/websafecolors/',
          img: '../../../static/img/websafecolors.png',
          content: '本表中列出的是 WEB 设计、开发中常用安全色。列于此是为了方便大家参考。'
        },
        {
          title: 'Pro Git',
          subhead: 'Git 入门到专家指南',
          url: 'https://yarn.bootcss.com/',
          img: '../../../static/img/progit.png',
          content: 'Pro Git 中文版（第二版）是一本详细的 Git 指南，主要介绍了 Git 的使用基础和原理，让你从 Git 初学者成为 Git 专家。'
        },
        {
          title: 'Nginx',
          subhead: '中文手册',
          url: 'https://nginx.bootcss.com',
          img: '../../../static/img/nginx.jpg',
          content: 'Nginx (engine x) 是一个高性能的HTTP和反向代理服务，也是一个IMAP/POP3/SMTP服务。'
        },
        {
          title: 'php工具箱',
          subhead: 'php程序员工具箱',
          url: 'http://tool.php.cn/',
          img: '../../../static/img/phptools.jpg',
          content: 'php程序员工具箱是迄今为止全网wei一一款php程序员的专属工具箱，集合了php环境搭建、在线小工具、原生手册、文字与视频教程、问答社区等。'
        },
        {
          title: '私人影院',
          subhead: 'move',
          url: 'http://www.aaqqw.com/',
          img: '../../../static/img/move.gif',
          content: '提供的最新电视剧和电影资源均系收集于各大视频网站'
        },
        {
          title: '斗鱼TV',
          subhead: '斗鱼直播',
          url: 'https://www.douyu.com/',
          img: '../../../static/img/douyu.jpg',
          content: '斗鱼- 每个人的直播平台提供高清、快捷、流畅的视频直播和游戏赛事直播服务,包含英雄联盟lol直播、穿越火线cf直播、dota2直播、美女直播等各类热门游戏赛事直播和各种...'
        },
        {
          title: '面试题',
          subhead: '面试题',
          url: 'https://github.com/Advanced-Frontend/Daily-Interview-Question/blob/master/datum/summary.md',
          img: '',
          content: '前端面试题及答案汇总'
        }
      ]
    }
  },
  mounted () {
    this.listenToUser()
    this.switchSearchEngin()
  },
  methods: {
    getNum (num) {
      var getOne = Math.ceil(Math.random() * num.length)
      return num[getOne]
    },
    // 编辑
    editBtn () {
      this.setIntervalData = setInterval(() => {
        this.editBtnData.left = this.getNum(this.leftArr) + 'px'
        this.editBtnData.top = this.getNum(this.topArr) + 'px'
        this.editBtnData.transform = 'rotate(' + this.getNum(this.rotateArr) + 'deg)'
      }, 20)
    },
    successBtn () {
      clearInterval(this.setIntervalData)
    },
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
      window.open(item.url, '_blank')
      // console.log(item)
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
  width: 80%;
  height: 70vh;
  margin: 0 auto;
  padding: 10px;
  overflow-y: scroll
}
#main::-webkit-scrollbar {display: none;}
</style>
