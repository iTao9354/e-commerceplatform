<template>
  <div class="index-wrap">
    <div class="index-left">
      <div class="index-left-block">
        <h2>全部产品</h2>
        <div class="index-left-info" :class="{'left-last-info': product.last}" v-for="product in productList">
          <h3>{{ product.title }}</h3>
          <ul class="index-left-list">
            <li v-for="item in product.list">
              <a :href="item.url">{{ item.title }}</a>
              <span v-if="item.hot" class="hot-tag">HOT</span>
            </li>
          </ul>
        </div>
      </div>
      <div class="index-left-block">
        <h2>最新消息</h2>
        <div class="index-left-info">
          <ul class="index-left-list">
            <li v-for="item in newsList">
              <a :href="item.url" :title="item.title">{{ item.title }}</a>
            </li>
          </ul>
        </div>
      </div>
    </div>
    <div class="index-right">
      <slide-show :slides="slides" :inv="invTime" @onchange="dosth"></slide-show>
      <ul class="index-board">
        <li :class="[{'board-item-even': index%2}, 'index-board'+item.id]" v-for="(item, index) in boardList">
          <div class="board-item-icon"></div>
          <div class="board-item-info">
            <h4>{{ item.title }}</h4>
            <p>{{ item.desc }}</p>
            <div class="board-item-btn">
              <a href="javascript:;">立即购买</a>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import slideShow from '../components/slideShow'
export default {
  components: {
    slideShow
  },
  data () {
    return {
      productList: {},   // 全部产品
      newsList: [],      // 最新消息
      boardList: [],     // 面板信息
      invTime: 2000,
      slides: [         // 幻灯片
        {
          'src': require('../assets/slideShow/pic1.jpg'),
          'title': 'xxx1',
          'href': 'detail/analysis'
        },
        {
          'src': require('../assets/slideShow/pic2.jpg'),
          'title': 'xxx2',
          'href': 'detail/count'
        },
        {
          'src': require('../assets/slideShow/pic3.jpg'),
          'title': 'xxx3',
          'href': 'http://xxx.xxx.com'
        },
        {
          'src': require('../assets/slideShow/pic4.jpg'),
          'title': 'xxx4',
          'href': 'detail/forecast'
        }
      ]
    }
  },
  created () {
    // 初始化全部产品
    this.initAllProducts()
    // 初始化最新消息
    this.initLatestNews()
    // 初始化面板信息
    this.initBoardList()
    // 初始化幻灯片信息
    // this.initSlides()
  },
  methods: {
    // 初始化全部产品
    initAllProducts () {
      this.$http.post('api/productList').then(res => {
        this.productList = res.data
      }, err => {
        console.log(err)
      })
    },
    // 初始化最新消息
    initLatestNews () {
      this.$http.post('api/newsList').then(res => {
        this.newsList = res.data
      }, err => {
        console.log(err)
      })
    },
    // 初始化面板信息
    initBoardList () {
      this.$http.post('api/boardList').then(res => {
        this.boardList = res.data
      }, err => {
        console.log(err)
      })
    },
    // 初始化幻灯片信息
    initSlides () {
      this.$http.post('api/slides').then(res => {
        this.slides = res.data
      }, err => {
        console.log(err)
      })
    },
    dosth (index) {
      // console.log('监听子组件幻灯片变化，当前为第' + (index + 1) + '张图')
    }
  }
}
</script>

<style scoped>
  .index-wrap {
    width: 1200px;
    margin: 0 auto;
    display: flex;
  }
  /* 左 */
  .index-left {
    flex: 240px;
    padding: 20px 15px;
  }
  .index-left-block {
    background: #fff;
    margin-bottom: 20px;
  }
  .index-left-block > h2 {
    height: 34px;
    line-height: 34px;
    background: #41b883;
    color: #fff;
    font-size: 16px;
    padding: 0 10px;
    font-weight: normal;
  }
  .index-left-info {
    padding: 0 10px;
    border-bottom: 1px solid #e0e0e0;
  }
  .left-last-info {
    border-bottom: none;
  }
  .index-left-info > h3 {
    margin-top: 15px;
  }
  .index-left-list {
    padding: 10px;
  }
  .index-left-list > li {
    max-width: 230px;
    height: 24px;
    line-height: 24px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
  .hot-tag {
    background: red;
    color: #fff;
    font-size: 12px;
  }

  /* 右 */
  .index-right {
    flex: 19;
    padding: 20px 0;
  }
  .index-board {
    display: flex;
    flex-wrap: wrap;
  }
  .index-board > li {
    width: calc(50% - 50px);
    background: #fff;
    margin: 0 20px 20px 0;
    padding: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .index-board > .board-item-even {
    margin-right: 0;
  }
  .board-item-icon {
    flex: 2;
    height: 100%;
    margin: 10px 15px 0 0;
    background-size: 100% auto;
    background-repeat: no-repeat;
    background-position: center center;
  }
  .index-board1 .board-item-icon {
    background-image: url(../assets/images/1.png);
  }
  .index-board2 .board-item-icon {
    background-image: url(../assets/images/2.png);
  }
  .index-board3 .board-item-icon {
    background-image: url(../assets/images/3.png);
  }
  .index-board4 .board-item-icon {
    background-image: url(../assets/images/4.png);
  }
  .board-item-info {
    flex: 8;
  }
  .board-item-info > h4 {
    line-height: 30px;
  }
  .board-item-info > p {
    font-size: 12px;
    margin-bottom: 10px;
  }
  .board-item-btn > a {
    display: inline-block;
    height: 20px;
    line-height: 20px;
    padding: 4px 12px;
    background: #41b883;
    color: #fff;
    font-size: 14px;
  }
</style>
