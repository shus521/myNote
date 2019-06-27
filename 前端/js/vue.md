[TOC]
## 穿透
 `/deep/` `>>>`
vue引用了第三方组件，需要在组件中局部修改第三方组件的样式，而又不想去除scoped属性造成组件之间的样式污染。此时只能通过>>>，穿透scoped。
有些Sass 之类的预处理器无法正确解析 `>>>`。可以使用 `/deep/` 操作符( `>>>` 的别名)
## 父组件传递数据给自组件
`prop` 是你可以在组件上注册的一些自定义特性。当一个值传递给一个 prop 特性的时候，它就变成了那个组件实例的一个属性
1. 子组件中添加props
```
export  default {
    name:  "server",
    data() {
        return {
            logo:  logo,
        }
    },
    props: ['packageList']
}
```
2. 父组件中`<server :packageList="packageList"></server>`即可在子组件中使用packageList
3. 动态绑定css样式
~~~
.bg {
  height: 220px;
  background: url("~@/assets/img/register/register.png") center top no-repeat;
}
~~~
## 发送短信倒计时效果
html部分
~~~
<a-button type="primary" :class="{disabled: !this.canClick}" @click="SendMessage">{{content}}</a-button>
~~~
js部分
~~~
export default {
  name: "register",
  data() {
    return {
      formLayout: 'horizontal',
      form: this.$form.createForm(this),
      content: '获取短信验证码',
      totalTime: 5,
      canClick: true
    }
  },
  methods: {
    SendMessage() {
      var phone = this.form.getFieldValue('mobile');
      if (!phone) {
        message.error('请输入手机号');
        return false;
      }
      var reg = /^1[3|4|5|7|8][0-9]{9}$/;

      var flag = reg.test(phone); //true
      if (!flag) {
        message.error('手机号格式不正确');
        return false;
      }
      this.countDown();
    },
    countDown () {
      if (!this.canClick) {
        return false;
      }
      this.canClick = false;
      this.content = this.totalTime + 's后重新发送';
      let clock = window.setInterval(() => {
        this.totalTime--;
        this.content = this.totalTime + 's后重新发送';
        if (this.totalTime < 0) {
          window.clearInterval(clock)
          this.content = '重新发送验证码';
          this.totalTime = 5;
          this.canClick = true
        }
      },1000)
    }
  },
};
~~~
css样式
~~~
.disabled{
  background-color: #ddd;
  border-color: #ddd;
  color:#57a3f3;
  cursor: not-allowed; // 鼠标变化
}
~~~