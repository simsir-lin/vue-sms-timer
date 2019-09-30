# vue-sms-timer
> 短信验证码倒计时

### 使用
1. 安装
```bash
npm install --save vue-sms-timer
```

2. 引入

```global
import Vue from 'vue'
import VueSmsTimer from 'vue-sms-timer'

Vue.component('VueSmsTimer', VueSmsTimer)
```

```something
import VueSmsTimer from 'vue-sms-timer'

const app = new Vue({
    components: { VueSmsTimer }
})
```

3. 添加
```
<vue-sms-timer :http-request="post" text="测试获取验证码" time="60" @start="handleStart" @end="handleEnd">
  <template v-slot="{ countDownText }">
    <button type="button" name="button">{{ countDownText }}</button>
  </template>
</vue-sms-timer>
```

### 调试开发
1. npm run serve
2. 参考 `/vue` 目录下

### Props

| name     | description              | type     | default value |
| :---------------- | :----------------------- | :------  | :------------ |
| http-request            |  获取验证码的http请求,必须返回true或Promise.resolve()                | function    |         |
| text             | 初始文本内容                 | String    | 获取验证码          |
| time            | 倒计时间(s)                 | Number    | 60          |

### events

| name     | description              | parameters     |
| :---------------- | :----------------------- | :------  |
| start            | 开始倒计时                 |     |
| end            | 结束倒计时                 |     |

### Slot

| name     | description              | scope     |
| :---------------- | :----------------------- | :------  |
| -            | 内容插槽                 | { countDownText }    |

### 贡献
如果你有好的意见或建议，欢迎给我提issue!

### TODO
* [x] 支持打开微信开放能力功能
