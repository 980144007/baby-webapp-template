<script setup>

</script>
<script>
import vConsole from "vconsole";
  export default {
    data() {
      return {
        vConsole: null,
        vT: null,
        clickNum: 0,
        vShow: JSON.parse(window.localStorage.getItem("vShow")) || false
      }
    },
    watch: {
      vShow(val) {
        window.localStorage.setItem("vShow", JSON.stringify(val));
        this.updateVConsole();
      }
    },
    methods: {
      updateVConsole() {
        if(!this.vShow) {
          if(!this.vConsole) return;
          this.vConsole.destroy();
          this.vConsole = null;
          return;
        }
        if(!this.vConsole) {
          this.vConsole = new vConsole();
        }
      },
      onAppClick() {
        clearTimeout(this.vT);
        this.clickNum++;
        if(this.clickNum >= 5) {
          this.vShow = !this.vShow;
        }
        // console.log(this.clickNum,this.vShow)
        this.vT = setTimeout(() => {
          this.clickNum = 0;
        }, 500);
      },
    },
    mounted() {
      this.updateVConsole();
      document.addEventListener("click", this.onAppClick);
    }
  }
</script>
<template>
  <div id="app-container">
    <router-view></router-view>
  </div>
</template>

<style lang="less">
html,body,#app,#app-container {
  width: 100%;
  height: 100%;
  padding: 0px;
  margin: 0px;
  box-sizing: border-box;
}
</style>
