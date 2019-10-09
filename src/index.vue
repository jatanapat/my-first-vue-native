<template>
  <root>
    <app-navigator></app-navigator>
  </root>
</template>

<script>
import {
  createAppContainer,
  createStackNavigator,
} from "vue-native-router";
import { Root } from "native-base";
import HomeScreen from "./screen/home.vue";
import CameraScreen from "./screen/camera.vue";
import FinishScreen from "./screen/finish.vue";

const StackNavigator = createStackNavigator(
  {
    Home: HomeScreen,
    Camera: CameraScreen,
    Finish: FinishScreen
  },
  {
    initialRouteName: 'Home',
    headerMode: "none"
  }
);

const AppNavigator = createAppContainer(StackNavigator);

export default {
  components: { Root, AppNavigator }
}
</script>