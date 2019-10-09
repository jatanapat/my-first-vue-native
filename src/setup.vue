<template>
  <view class="container">
    <app v-if="isReady"></app>
  </view>
</template>

<script>
import Vue from "vue-native-core";
import { VueNativeBase } from "native-base";
import App from "./index.vue";

Vue.use(VueNativeBase);

export default {
  data: function () {
    return {
      isReady: false
    }
  },
  created: function () {
    this.loadAppFonts();
  },
  methods: {
    loadAppFonts: async function () {
      try {
        this.isReady = false;
        await Expo.Font.loadAsync({
          Roboto: require("../node_modules/native-base/Fonts/Roboto.ttf"),
          Roboto_medium: require("../node_modules/native-base/Fonts/Roboto_medium.ttf")
        });
        this.isReady = true;
      } catch (error) {
        console.log("Can't load fonts", error);
        this.isReady = true;
      }
    },
  },
  components: { App }
};
</script>

<style>
.container {
  flex: 1;
}
</style>