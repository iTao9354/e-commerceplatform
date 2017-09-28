<template>
  <div class="container">
    <div class="app-head">
      <div class="app-head-inner">
        <img src="../assets/logo.png" alt="">
        <div class="head-nav">
          <ul class="nav-list">
            <li>登录</li>
            <li class="nav-pile">|</li>
            <li>注册</li>
            <li class="nav-pile">|</li>
            <li>关于</li>
          </ul>
        </div>
      </div>
    </div>
    <div class="app-content">
      <keep-alive>
        <router-view></router-view>
      </keep-alive>
    </div>
    <div class="app-foot">这里是底部</div>
  </div>
</template>

<script>
export default {

}
</script>

<style>
  .container {
    width: 100%;
    display: flex;
    flex-direction: column;
  }
  /* 头部 */
  .app-head {
    flex: 1;
    background-color: #504f4f;
    color: #b2b2b2;
    height: 60px;
    line-height: 60px;
  }
  .app-head-inner {
    width: 1200px;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
  }
  .app-head-inner > img {
    height: 30px;
    margin-top: 15px;
  }
  .nav-list {
    display: flex;
  }
  .nav-list > li:not(.nav-pile) {
    flex: 1;
    padding: 0 10px;
    cursor: pointer;
  }

  /* 内容区 */
  .app-content {
    min-height: calc(100vh - 140px);
    display: flex;
    flex: 1;
  }

  /* 底部 */
  .app-foot {
    flex: 1;
    height: 80px;
    background: #e3e4e8;
    text-align: center;
    line-height: 80px;
  }
</style>


