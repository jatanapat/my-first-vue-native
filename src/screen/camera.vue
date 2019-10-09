<template>
  <view class="container">
    <view class="header">
      <text v-if="rndIndex === 0" class="text-color-white">กรุณาถ่ายภาพหน้าตรง</text>
      <text v-if="rndIndex === 1" class="text-color-white">กรุณาหันหน้าไปทางขวา</text>
      <text v-if="rndIndex === 2" class="text-color-white">กรุณาหันหน้าไปทางซ้าย</text>
      <text v-if="rndIndex === 3" class="text-color-white">กรุณาเอียงคอไปทางขวา</text>
      <text v-if="rndIndex === 4" class="text-color-white">กรุณาเอียงคอไปทางซ้าย</text>
      <text v-if="rndIndex === 5" class="text-color-white">กรุณามองขึ้นด้านบน</text>
      <text v-if="rndIndex === 6" class="text-color-white">กรุณามองลงด้านล่าง</text>
    </view>
    <image class="pose"
      v-if="rndIndex"
      :source="pose[rndIndex]"
    />
    <camera class="container" :type="type" ref="camera">
      <view class="footer">
        <touchable-opacity :on-press="takePic">
          <view class="snap-btn">
            <view class="inner-snap-btn">
              <text :style="{color: '#ea3223', fontSize: 26}">{{countDown}}</text>
            </view>
          </view>
        </touchable-opacity>
      </view>
    </camera>
  </view>
</template>

<script>
import * as Permissions from 'expo-permissions';
import { Camera } from "expo-camera";

export default {
  data() {
    return {
      timeCD: 0,
      rndIndex: 0,
      numbers: [1, 2, 3, 4, 5, 6],
      countDown: 9,
      pose: ['',
        require('../../assets/pose/turn_left.png'),
        require('../../assets/pose/turn_right.png'),
        require('../../assets/pose/lean_left.png'),
        require('../../assets/pose/lean_right.png'),
        require('../../assets/pose/look_above.png'), 
        require('../../assets/pose/look_below.png')
      ],
      captures: [],
      hasCameraPermission: false,
      type: Camera.Constants.Type.front
    };
  },
  mounted() {
    Permissions.askAsync(Permissions.CAMERA)
      .then(status => {
        hasCameraPermission = status.status == "granted" ? true : false;
      })
      .then(() => {
        this.setTimeCountDown();
      }).catch((err)=>{
          console.log(err);
      });
  },
  props: {
    navigation: {
      type: Object
    }
  },
  methods: {
    takePic() {
      if (this.$refs.camera) {
        this.$refs.camera.takePictureAsync()
          .then((data) => {
            console.log(data);
            this.captures.push(data.uri);
            console.log(this.captures);
            if (this.captures.length < 3) {
              this.rndIndex = this.getRandomIndex(this.numbers);
              clearInterval(this.timeCD);
              this.countDown = 9;
              this.setTimeCountDown();
            } else {
              this.navigation.navigate("Finish");
            }
          });
      }
    },
    getRandomIndex(array) {
      const index = Math.floor(Math.random() * array.length);
      const rand = array[index];
      this.numbers.splice(index, 1);
      return rand;
    },
    setTimeCountDown() {
      this.timeCD = setInterval(() => {
        this.countDown -= 1;
        if (this.countDown <= 0) {
          clearInterval(this.timeCD);
          this.takePic();
        }
      }, 1000);
    }
  },
  components: { Camera },
};
</script>

<style>
.container {
  flex: 1;
  justify-content: space-between;
}
.header {
  width: 100%;
  height: 100;
  background-color: #4b99f4;
  align-items: center;
  justify-content: center;
}
.text-color-white {
  color: white;
  font-size: 16;
}
.pose {
  position: absolute;
  top: 120;
  left: 20;
  z-index: 2;
  width: 100;
  height: 100;
}
.footer {
  position: absolute;
  bottom: 10;
  left: 42%;
  flex-direction: row;
  justify-content: space-around;
}
.snap-btn {
  width: 64;
  height: 64;
  border-radius: 32;
  border-width: 8;
  border-color: #808080;
  justify-content: center;
  align-items: center;
}
.inner-snap-btn {
  background-color: white;
  width: 52;
  height: 52;
  border-radius: 25.5;
  justify-content: center;
  align-items: center;
}
</style>