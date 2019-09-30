<template>
  <div class="sms-code" @click="send">
    <slot :countDownText="countDownText">{{ countDownText }}</slot>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class VueSmsCode extends Vue {
  @Prop() private httpRequest!: any;
  @Prop({ default: "获取验证码" }) private text?: string;
  @Prop({ default: 60 }) private time?: number;
  countDownText: string | undefined = "";
  timerRunning: boolean = false;
  timer: number = 0;
  remainTime: number | undefined = 0;

  created() {
    this.countDownText = this.text;
  }

  send() {
    if (this.timerRunning) {
      return;
    }
    if (this.httpRequest) {
      this.countDownText = "获取中";
      const httpRequest = this.httpRequest();
      if (httpRequest) {
        this._startTimer();
        return;
      }
      httpRequest.then(() => {
        this._startTimer();
      });
    }
  }

  _startTimer() {
    this.timerRunning = true;
    this.remainTime = this.time;
    this.$emit("start");
    this.timer = window.setInterval(() => {
      if (this.remainTime === 1) {
        this.timerRunning = false;
        this.countDownText = this.text;
        clearInterval(this.timer);
        this.$emit("end");
        return;
      }
      this.remainTime = Number(this.remainTime) - 1;
      this.countDownText = this.remainTime + "s重新获取";
    }, 1000);
  }
}
</script>

<style scoped lang="scss">
.sms-code:hover {
  cursor: pointer;
}
</style>
