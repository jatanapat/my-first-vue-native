<template>
  <view class="container">
    <view :style="{width: 300, height: 450, backgroundColor: 'white', borderWidth: 0, borderRadius: 5, fontSize: 16,alignItems: 'center',
      justifyContent: 'center'}">
      <ionicons name="md-checkmark" :size="160" :color="'#4b99f4'" :style="{paddingBottom:40}"/>
      <text class = "text-primary" :style="{paddingBottom:20}">ยืนยันตัวตนสำเร็จ</text>
      <touchable-opacity class="button-container" :on-press="goToHome">
        <text :style="{color: 'white'}">OK</text>
      </touchable-opacity>
    </view>
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
    goToHome() {
      this.navigation.navigate("Home");
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
}
.button-container {
  width: 40%;
  height: 40;
  background-color: #4b99f4;
  align-items: center;
  justify-content: center;
  border-radius: 2;
  margin-top: 40;
}
</style>