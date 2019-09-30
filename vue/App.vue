<template>
  <div id="app">
    <vue-sms-code
      :http-request="post"
      text="测试获取验证码"
      @start="handleStart"
      @end="handleEnd"
    >
      <template v-slot="{ countDownText }">
        <button type="button" name="button">{{ countDownText }}</button>
      </template>
    </vue-sms-code>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import VueSmsCode from "../src/vue-sms-code.vue";

@Component({
  components: {
    VueSmsCode
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
  handleStart() {
    console.log("handleStart");
  }
  handleEnd() {
    console.log("handleEnd");
  }
}
</script>
