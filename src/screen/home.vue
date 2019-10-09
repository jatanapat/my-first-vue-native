<template>
  <view class="container">
    <text class = "text-primary" :style="{flexDirection: 'row'}">กรุณายืนยันตัวตน</text>
    <view :style="{flexDirection: 'row',width: 350, height: 350, marginTop: 50, backgroundColor: 'white', borderRadius: 350, borderColor: '#f9fcff', borderWidth: 40, alignItems: 'center', justifyContent: 'center', fontSize: 16}">
      <ionicons name="md-person" :size="160" :color="'#4b99f4'"/>
    </view>
    <text class = "text-primary" :style="{marginTop: 50}">กรุณาทำตามขั้นตอนยืนยันตัวตน</text>
    <text class = "text-primary">ด้วยการถ่ายภาพ 3 ภาพ</text>
    <text class = "text-primary">ตามท่าทางที่ระบุ</text>
    <touchable-opacity class="button-container" :style="{flexDirection: 'row', marginTop: 30}" :on-press="goToCamera">
      <text :style="{color: 'white', fontSize: 14}">เริ่ม</text>
    </touchable-opacity>
  </view>
</template>

<script>
import { Ionicons  } from '@expo/vector-icons';

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
  },
  components: { Ionicons }
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