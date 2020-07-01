<template>
  <div class="qrcodeBtn" @mousedown.stop="showQrCode">
  	手机阅读
    <qrcode-vue id='qrcodeContainer'  v-if="show" ref="qrcodeContainer" :value="qrcodeText" :size="size" level="H"></qrcode-vue>
  </div>
</template>

<script>
// import QRCode from 'qrcodejs2'
import QrcodeVue from 'qrcode.vue'
export default {
  components: {
    QrcodeVue,
  },
  data(){
  	return {
  		show:false,
      qrcodeText: '',
      size: 100,
  	}
  },
  mounted(){
	  document.documentElement.addEventListener("mousedown", ()=>{
		  this.show = false;
	  });
  },
  methods:{
  	showQrCode(){
  		this.show = !this.show;

  		if(this.show){
  			this.$nextTick(()=>{
  				this.qrcodeText = location.href;
  			})
  		}
  	}
  }
}
</script>

<style lang="stylus">
.qrcodeBtn
  position relative
  margin-left 15px

  &:hover
    color $accentColor
    cursor pointer
  #qrcodeContainer
  	width 100px
  	height 100px
  	position absolute
  	right 0
  	top 50px
</style>
