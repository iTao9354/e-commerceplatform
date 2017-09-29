<template>
  <div>
    <div class="app-head">
      <div class="app-head-inner clearfix">
        <img src="../assets/logo.png" alt="">
        <div class="head-nav fr">
          <ul class="nav-list">
            <li>{{ username }}</li>
            <li v-if="!username" @click="logClick">登录</li>
            <li class="nav-pile">|</li>
            <li v-if="username" @click="quit">退出</li>
            <li v-if="!username" @click="resClick">注册</li>
            <li class="nav-pile">|</li>
            <li @click="aboutClick">关于</li>
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
    <!-- 弹出层 -->
    <my-dialog :is-show="isShowLogDialog" @on-close="closeDialog('isShowLogDialog')">
      <log-form @has-log="onSuccessLog"></log-form>
    </my-dialog>
    <my-dialog :is-show="isShowResDialog" @on-close="closeDialog('isShowResDialog')">
      <res-form></res-form>
    </my-dialog>
    <my-dialog :is-show="isShoAboutDialog" @on-close="closeDialog('isShoAboutDialog')">
      <p>本报告在调研数据的基础上，采用定性与定量相结合的方式深入分析了专车市场发展的驱动因素与阻碍因素、专车市场背后的产业格局、专车企业的竞争格局、用户对专车市场的依赖程度、专车对其他交通工具运力的补充效应等，通过这五个章节的研究反映专车市场的发展态势和面临的问题。报告力求客观、深入、准确地反映中国专车市场发展情况，为政府、企事业单位和社会各界提供决策依据。 </p>
    </my-dialog>
  </div>
</template>

<script>
import MyDialog from './dialog'
import LogForm from './logForm'
import ResForm from './resForm'
export default {
  components: {
    MyDialog,
    LogForm,
    ResForm
  },
  data () {
    return {
      isShowLogDialog: false,     // “登录”弹出层
      isShowResDialog: false,     // “注册”弹出层
      isShoAboutDialog: false,    // “关于”弹出层
      username: ''
    }
  },
  methods: {
    logClick () {
      this.isShowLogDialog = true
    },
    resClick () {
      this.isShowResDialog = true
    },
    aboutClick () {
      this.isShoAboutDialog = true
    },
    closeDialog (attr) {
      this[attr] = false
    },
    onSuccessLog (data) {
      this.username = data.username
      this.closeDialog('isShowLogDialog')
    }
  }
}
</script>

<style>
  /* 头部 */
  .app-head {
    background-color: #504f4f;
    color: #b2b2b2;
    height: 60px;
    line-height: 60px;
  }
  .app-head-inner {
    width: 1200px;
    margin: 0 auto;
  }
  .app-head-inner > img {
    height: 30px;
    margin-top: 15px;
  }
  .nav-list {
    display: flex;
  }
  .nav-list > li:not(.nav-pile) {
    padding: 0 10px;
    cursor: pointer;
  }

  /* 内容区 */
  .app-content {
    min-height: calc(100vh - 140px);
  }

  /* 底部 */
  .app-foot {
    height: 80px;
    background: #e3e4e8;
    text-align: center;
    line-height: 80px;
  }

  /* 弹出层 */
  .g-form-line {
    padding: 15px 0;
  }
  .g-form-label {
    width: 100px;
    font-size: 16px;
    display: inline-block;
  }
  .g-form-input {
    display: inline-block;
  }
  .g-form-input input {
    height: 30px;
    width: 200px;
    line-height: 30px;
    vertical-align: middle;
    padding: 0 10px;
    border: 1px solid #ccc;
  }
  .g-form-btn {
    padding-left: 100px;
  }
  .g-form-btn .button {
    margin-left: 2px;
    padding: 5px 20px;
    color: #fff;
    background: #41b883;
  }
  .g-form-error {
    color: red;
    padding-left: 15px;
  }
</style>


