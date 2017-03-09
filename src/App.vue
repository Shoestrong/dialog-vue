<template>
  <div id="app">
  <div>
    <p>普通弹框</p>
    <button type="button" class="primary-btn" @click="alertNormal">Alert</button>
    <button type="button" class="primary-btn" @click="confirmNormal">confirm</button>
    <p>设置title</p>
    <button type="button" class="primary-btn" @click="alertTitle">Alert</button>
    <button type="button" class="primary-btn" @click="confirmTitle">confirm</button>
    <p>自定义按钮文本</p>
    <button type="button" class="primary-btn" @click="alertBtn">Alert</button>
    <button type="button" class="primary-btn" @click="confirmBtn">confirm</button>
    <p>按钮点击事件</p>
    <button type="button" class="primary-btn" @click="alertCallback">Alert</button>
    <button type="button" class="primary-btn" @click="confirmCallback">confirm</button>
  </div>
    <router-view></router-view>
  </div>
</template>

<script>
import Vue from 'vue'
import dialog from './components/Dialog'

export default {
  name: 'app',
  methods:{
    alertNormal(){
        new Vue(dialog).alert();
    },
    confirmNormal(){
        new Vue(dialog).confirm("我就是一个普通弹框");
    },
    alertTitle(){
        new Vue(dialog).alert('','alert我改变了title');
    },
    confirmTitle(){
        new Vue(dialog).confirm('','confirm我改变了title');
    },
    alertBtn(){
        new Vue(dialog).alert('内容区域','title自定义按钮文本');
    },
    confirmBtn(){
        new Vue(dialog).confirm({
            title: '提示',
            message: '您尚未登录',
            confirmButtonText: '去登陆',
            cancelButtonText: '我只是路过',
            onConfirm(){
                new Vue(dialog).alert('登录失败');
            }
        })
    },
    alertCallback(){
        new Vue(dialog).alert({
            message: '提醒内容',
            onConfirm(){
                window.alert('点击了按钮，调用this.close()可以关闭');
                this.close();
            }
        })
    },
    confirmCallback(){
        new Vue(dialog).confirm('提示内容',null,function(){
            window.alert('你确认？');
        },function(){
            window.alert('你点击了取消');
            this.close();
        })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.primary-btn:hover{
    background-color: #a3cdea;
}
.primary-btn{
    background-color: #71A2C1;
    color:#fff;
    padding: 8px 15px;
    font-size: 16px;
    border:0;
    outline: none;
    border-radius: 5px;
}
</style>
