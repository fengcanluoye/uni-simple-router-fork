<template>
  <view class="content">
    <image class="logo" src="/static/logo.png"></image>
    <view class="text-area">
      <text class="title">{{ title }}</text>
    </view>
    <!-- 		<div>
			<childComponent></childComponent>
		</div>
		<button type="default" @click="gotoPage">点我去page2</button>
		<button type="primary" @click="gotoPage1('../page4/page4')">传递中文</button>
		<button type="warn" @click="gotoPage1('/pages/builtIn/builtIn')">点我去获取内置地址</button> -->

    <!-- #ifdef MP-WEIXIN -->
    <button type="default" @click="forceEach">
      微信小程序看到我，强制触发
    </button>
    <!-- #endif -->

    <!-- 		
		<button type="primary" @click="$router.push({name:'nvue1'})">去nvue1测试页</button>
		
		<button type="primary" @click="gotoTabPage">去tab2测试页面</button>
		<button type="default" @click="gotoPage2">深度传参</button> -->
  </view>
</template>

<script>
import childComponent from '../../common/com/com.vue'
export default {
  components: {
    childComponent,
  },
  data() {
    return {
      title: 'Hello',
    }
  },
  onTabItemTap() {
    console.log('@@@@@@@@@@@@@-----tab1页面被点击------@@@@@@@@@@@@')
  },
  beforeMount() {
    console.log('index-----beforeMount')
  },
  created() {
    console.log('index-----created')
  },
  mounted() {
    console.log('index-----mounted')
  },
  onReady() {
    console.log('index-----onReady')
  },
  onLoad(e) {
    console.log(e)
    console.log('index-----onload')
  },
  onShow() {
    console.log('index-----onShow')
  },
  computed: {
    Route() {
      return this.$route
    },
  },
  methods: {
    gotoTabPage() {
      this.$router.pushTab({
        path: '/pages/other/other',
        success: (...args) => {
          console.log(args)
          console.log('tab2跳转成功')
        },
        complete: () => {
          console.log('tab2跳转结束')
          console.log(this.title)
        },
        fail: () => {
          console.log('tab2跳转失败')
        },
      })
    },
    forceEach() {
      this.$router.forceGuardEach()
    },
    gotoPage1(url = '/pages/page4/page4') {
      uni.navigateTo({
        url: `${url}?msg=的挥洒U盾好撒第三大厦发的撒321312*（￥#4`,
        events: {
          acceptDataFromOpenedPage: function (data) {
            console.log(data)
          },
          someEvent: function (data) {
            console.log(data)
          },
        },
        success: (res) => {
          console.log(res)
          res.eventChannel.emit('acceptDataFromOpenerPage', { data: 'test' })
          console.log('跳转成功')
        },
      })
    },
    gotoPage2() {
      this.$router.push({
        path: '/beforeRouteLeave',
        query: {
          targetyutk: 0,
          result: '你好',
          jumpWay: '0',
          测试: '666',
          // status:true,
          // list:[
          // 	{
          // 		id:1,
          // 		name:333
          // 	},
          // ]
        },
      })
    },
    gotoPage() {
      // this.$router.push({
      // 	name:'page2',
      // 	params:{
      // 		id:6666
      // 	}
      // })

      this.$router.push({
        success: (...args) => {
          console.log(args)
          console.log('跳转成功')
          console.log(this.title)
        },
        complete: () => {
          console.log('跳转结束')
          console.log(this.title)
        },
        fail: () => {
          console.log('跳转失败')
        },
        name: 'page2',
        params: {
          id: 12,
        },
      })

      // uni.navigateTo({
      // 	url:'/pages/navigate/navigate?id=555&name=hhyang',
      // 	success:()=>{
      // 		console.log('跳转成功')
      // 	},
      // })
    },
  },
}
</script>

<style>
.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.logo {
  height: 200rpx;
  width: 200rpx;
  margin-top: 200rpx;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 50rpx;
}

.text-area {
  display: flex;
  justify-content: center;
}

.title {
  font-size: 36rpx;
  color: #8f8f94;
}
</style>
