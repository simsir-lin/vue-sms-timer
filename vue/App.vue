<template>
  <div id="app">
    <vue-sms-timer
      :http-request="post"
      text="测试获取验证码"
      @start="handleStart"
      @end="handleEnd"
    >
      <template v-slot="{ countDownText }">
        <button type="button" name="button">{{ countDownText }}</button>
      </template>
    </vue-sms-timer>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import VueSmsTimer from "../src/vue-sms-timer.vue";

@Component({
  components: {
    VueSmsTimer
  }
})
export default class App extends Vue {
  post() {
    // return true
    return new Promise((resolve, reject) => {
      setTimeout(function() {
        resolve();
      }, 500);
    });
  }
  handleStart() {}
  handleEnd() {}
}
</script>
