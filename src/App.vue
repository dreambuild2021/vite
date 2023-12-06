<script setup>
import axios from 'axios'
import {ref} from 'vue'

const result = ref('')

async function wxInit() {
  const res = await axios.get('https://service-bg08w8zt-1302038052.bj.tencentapigw.com/release/config', {
    params: {
      url: location.href.split('#')[0]
    }
  })
  window.wx.config({
    debug: true,
    appId: 'wxaffacb192aae22ff',
    timestamp: res.data.timestamp,
    nonceStr: res.data.nonceStr,
    signature: res.data.signature,
    jsApiList: ['scanQRCode']
  })
}

wxInit()

async function handleClick() {
  window.wx.scanQRCode({
    needResult: 1,
    scanType: ["qrCode"],
    success: function (res) {
      console.log(res)
      result.value = res.resultStr;
    }
  });
}
</script>

<template>
  <div>
    <button @click="handleClick">扫一扫</button>
    <hr />
    扫描结果：{{ result }}
  </div>
</template>

<style scoped>
button {
  display: block;
  width: 100%;
}
</style>
