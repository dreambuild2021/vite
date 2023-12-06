<script setup>
import axios from 'axios'

async function wxInit() {
  const res = await axios.get('https://service-bg08w8zt-1302038052.bj.tencentapigw.com/release/config')
  wx.config({
    debug: true,
    appId: 'wx03ec3333acc0b717',
    timestamp: res.data.timestamp,
    nonceStr: res.data.nonceStr,
    signature: res.data.signature,
    jsApiList: ['scanQRCode']
  });
  wx.ready(() => {
    alert('ready')
  })
  wx.error((err) => {
    console.log('err', err)
  })
}

wxInit()

async function handleClick() {
  wx.scanQRCode({
    needResult: 1,
    scanType: ["qrCode"],
    success: function (res) {
      var result = res.resultStr;
      alert(result)
    }
  });
}
</script>

<template>
  <div>
    <button @click="handleClick">扫一扫</button>
  </div>
</template>

<style scoped></style>
