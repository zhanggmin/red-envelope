<template>
  <div class="play_text_page">
    <!-- 拼字详细情况 -->
    <div class="text_content">
      {{textContent}}
    </div>
    <div class="game_times">
      {{gameTime}}<span>s</span>
    </div>
    <div class="game_tips">
      请根据以上文字顺序拼出文字顺序抢红包哦稍后文字顺序将会打乱
    </div>
    <div class="start_games" @click="startGames()">
      立即开始
    </div>
  </div>
</template>

<script>

export default {
  components: {
  },

  data () {
    return {
      textContent: '',
      gameTime: 30
    }
  },
  methods: {
    startGames () {
      const url = `../../../play-detail/text/playing/main?content=${this.textContent}&id=${this.id}&gameTime=${this.gameTime}`
      wx.redirectTo({url})
    }
  },
  created () {
  },
  onLoad () {
    this.textContent = this.$root.$mp.query.content
    this.id = this.$root.$mp.query.id
    this.gameTime = this.$root.$mp.query.gameTime
  }
}
</script>

<style>
.play_text_page{
  width: 100%;
  height: 100%;
  position: fixed;
  overflow: scroll;
}
.text_content{
  padding-top: 100rpx;
  text-align: center;
  height: 50%;
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
