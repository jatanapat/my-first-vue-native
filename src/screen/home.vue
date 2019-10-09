<template>
  <view class="container">
    <text class = "text-primary" :style="{top:50, position: 'absolute'}">กรุณายืนยันตัวตน</text>
    <view :style="{width: 350, height: 350, backgroundColor: 'white', borderRadius: 350, borderColor: '#f9fcff', borderWidth: 40, alignItems: 'center', justifyContent: 'center', fontSize: 16}">
      <nb-icon name="person" :style="{fontSize: 160, color: '#4b99f4'}"/>
    </view>
    <text class = "text-primary" :style="{marginTop:90}">กรุณาทำตามขั้นตอนยืนยันตัวตน</text>
    <text class = "text-primary">ด้วยการถ่ายภาพ 3 ภาพ</text>
    <text class = "text-primary">ตามท่าทางที่ระบุ</text>
    <touchable-opacity class="button-container" :style="{bottom:30, position: 'absolute'}" :on-press="goToCamera">
      <text :style="{color: 'white', fontSize: 14}">เริ่ม</text>
    </touchable-opacity>
  </view>
</template>

<script>
export default {
  props: {
    navigation: {
      type: Object
    }
  },
  methods: {
    goToCamera() {
      this.navigation.navigate("Camera");
    }
  }
}
</script>

<style>
.container {
  background-color: #f2f9fe;
  align-items: center;
  justify-content: center;
  flex: 1;
}
.text-primary {
  color: #4b99f4;
  font-size: 16;
  font-weight: bold;
}
.button-container {
  width: 70%;
  height: 40;
  background-color: #4b99f4;
  align-items: center;
  justify-content: center;
  border-radius: 2;
}
</style>