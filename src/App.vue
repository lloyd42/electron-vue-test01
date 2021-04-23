<template>
  <div id="app">
    <div class="frame">
      <button @click="min" class="min" type="button">
        <i class="iconfont icon-zuixiaohua_line_1"></i>
      </button>
      <button @click="max" class="max" type="button">
        <i
          class="iconfont"
          :class="[isMax ? 'icon-huanyuan_line_1' : 'icon-zuidahua_line_1']"
        ></i>
      </button>
      <button @click="close" class="close" type="button">
        <i class="iconfont icon-guangbi_line_1"></i>
      </button>
    </div>
    <div class="content">
      <img alt="Vue logo" src="./assets/logo.png" />
      <HelloWorld msg="Welcome to Your Vue.js App" />
    </div>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import { remote, ipcRenderer } from "electron";

export default {
  name: "App",
  components: {
    HelloWorld,
  },
  data() {
    return {
      isMax: false,
    };
  },
  methods: {
    min() {
      //ipcRenderer.send("min");
      remote.getCurrentWindow().minimize();
    },
    max() {
      ipcRenderer.send("max");
      if (remote.getCurrentWindow().isMaximized()) {
        this.isMax = true;
      } else {
        this.isMax = false;
      }
    },
    close() {
      //ipcRenderer.send("close");
      remote.getCurrentWindow().close();
      //console.log("123");
    },
  },
};
</script>

<style>
@import url("assets/css/iconfont.css");
body {
  margin: 0;
  padding: 0;
  overflow: hidden;
  /* 配合background.js设置背景透明，这是得到圆角边框的基础条件 
     在chrome的调试模式下圆角会无效。
  */
  background: #ffffff00;
  /* background-color: rgba(0, 0, 0, 0); */
  border: 0;
}
body::-webkit-scrollbar {
  display: none;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  height: 100%;
  border-radius: 10px;
  background-color: teal;
}
.frame {
  height: 40px;
  /* width: 100%; */
  -webkit-app-region: drag;
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  background-color: wheat;
  border-radius: 10px 10px 0 0;
}
.frame button {
  color: teal;
  font-size: 20px;
  border: 0;
  background: transparent;
  -webkit-app-region: no-drag !important;
  outline: none;
}
button.close {
  border-radius: 0 10px 0 0;
}
.content {
  /* flex: 1; */
  height: calc(100vh - 40px);
  height: -webkit-calc(100vh - 40px);
  height: -moz-calc(100vh - 40px);
  width: 100%;
  overflow-y: scroll !important;
}
.content::-webkit-scrollbar {
  width: 0 !important;
}
</style>
