<template>
  <div class="play_pic_page">
    <!-- 拼字详细情况 -->
    <div class="text_content">
      <canvas class="canvas_picture" :style=canvasStyles canvas-id="startPic"></canvas>
    </div>
    <div class="game_times">
      {{gameTime}}<span>s</span>
    </div>
    <div class="game_tips">
      请根据以上图片拼出图片抢红包哦<br/>稍后图片顺序将会打乱
    </div>
    <div class="start_games" @click="startGames()">
      立即开始
    </div>
  </div>
</template>

<script>
import { getBasicBlockInfo, getInitPositionList, piecesImage, getImageInfo } from '../../../../utils/index'
export default {
  components: {
  },

  data () {
    return {
      imgSource: '',
      gameTime: '',
      level: '',
      levelMap: {
        1: 3,
        2: 4,
        3: 5
      },
      canvasStyles: `width: 315px`,
      windowHeight: 603, // 默认iphone 6 尺寸
      windowWidth: 375 // 默认iphone 6 尺寸
    }
  },
  methods: {
    startGames () {
      const url = `../../../play-detail/picture/playing/main?content=${this.imgSource}&id=${this.id}&gameTime=${this.gameTime}&level=${this.level}`
      wx.redirectTo({url})
    }
  },
  created () {
  },
  async onLoad () {
    this.imgSource = this.$root.$mp.query.content
    let loadImgSrc = await getImageInfo(this.imgSource) // 下载图片到本地
    this.id = this.$root.$mp.query.id
    this.gameTime = this.$root.$mp.query.gameTime
    this.level = this.$root.$mp.query.level
    let imgOption = getBasicBlockInfo(this, this.levelMap[this.level], loadImgSrc.height)
    let imageInfos = getInitPositionList(imgOption)
    console.log('loadImgSrc', loadImgSrc)
    piecesImage('startPic', loadImgSrc.path, imageInfos)
  }
}
</script>

<style>
.play_pic_page{
  width: 100%;
  height: 100%;
  position: fixed;
}
.canvas_picture{
  margin: 2% 6.7%;
  /* text-align: center; */
  /* margin: 22rpx auto; */
}
.text_content{
  position: relative;
  height: 60%;
  font-size:36rpx;
  font-weight:400;
  color:rgba(0,0,0,1);
}
.game_times{
  width:168rpx;
  height:168rpx;
  background:rgba(255,67,71,1);
  box-shadow:3rpx 3rpx 4rpx 0rpx rgba(193,190,190,0.82);
  border-radius:84rpx;
  font-size:68rpx;
  font-weight:400;
  margin: 0 auto;
  color:rgba(255,255,255,1);
  line-height: 168rpx;
  text-align: center;
}
.game_times span{
  font-size:36rpx;
}
.game_tips{
  width: 72%;
  padding: 56rpx 0;
  margin: 0 auto;
  text-align: center;
  font-size:28rpx;
  font-weight:400;
  color:rgba(0,0,0,1);
}
.start_games{
  height:88rpx;
  width: 87%;
  background:rgba(255,67,71,1);
  box-shadow:3rpx 3rpx 4rpx 0rpx rgba(193,190,190,0.82);
  border-radius:44rpx;
  margin: 0 auto;
  text-align: center;
  line-height: 88rpx;
  font-size:32rpx;
  font-weight:400;
  color:rgba(255,255,255,1);
}
</style>
