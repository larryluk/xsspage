<template>
  <div id="nav" class="base">
    <el-menu
      class="el-menu-vertical-demo"
      @open="handleOpen"
      @close="handleClose">
      <el-menu-item index="1" @click='searchBook'>
        <i class="el-icon-search"></i>
        <span slot="title">搜索小说</span>
      </el-menu-item>
      <el-menu-item index="2" v-on:click="menuSwitch(false)">
        <i class="el-icon-back"></i>
        <span slot="title">关闭</span>
      </el-menu-item>
    </el-menu>
    </div>
</template>



<style>
#nav {
  height: 100%;
  width: 150px;
  position: absolute;
  z-index: 999;
  top: 0px;
  background: aqua;
}

#back {
  float:right;
}

#nav el-menu {
  width: 150px;
}

.fadeIn {
  animation: navFadeIn 0.5s;
  -moz-animation: navFadeIn 0.5s;	/* Firefox */
  -webkit-animation: navFadeIn 0.5s;	/* Safari 和 Chrome */
  -o-animation: navFadeIn 0.5s;	/* Opera */
  left: 0px;
}

.base {
  left: -150px;
}

.fadeOut {
  animation: navFadeOut 0.5s;
  -moz-animation: navFadeOut 0.5s;	/* Firefox */
  -webkit-animation: navFadeOut 0.5s;	/* Safari 和 Chrome */
  -o-animation: navFadeOut 0.5s;	/* Opera */
  left: -150px;

}


//打开动画
@keyframes navFadeIn
{
from {left: -150px;}
to {left: 0px;}
}

@-moz-keyframes navFadeIn /* Firefox */
{
from {left: -150px;}
to {left: 0px;}
}

@-webkit-keyframes navFadeIn /* Safari 和 Chrome */
{
from {left: -150px;}
to {left: 0px;}
}

@-o-keyframes navFadeIn /* Opera */
{
from {left: -150px;}
to {left: 0px;}
}

//关闭动画
@keyframes navFadeOut
{
from {left: 0px;}
to {left: -150px;}
}

@-moz-keyframes navFadeOut /* Firefox */
{
from {left: 0px;}
to {left: -150px;}
}

@-webkit-keyframes navFadeOut /* Safari 和 Chrome */
{
from {left: 0px;}
to {left: -150px;}
}

@-o-keyframes navFadeOut /* Opera */
{
from {left: 0px;}
to {left: -150px;}
}

</style>


<script>
import nav from './Nav.vue'
import axios from 'axios'

export default {
  components: {
    'nav': nav
  },
  methods: {
    menuSwitch: function(sw) {
      this.$el.attributes.class.value = "";

      //true 打开动画 false 关闭动画
      if(!sw) {
        //todo:关闭动画
        this.$el.attributes.class.value = "fadeOut";

      } else {
        //todo:打开动画
        this.$el.attributes.class.value = "fadeIn";

      }
    },
    searchBook: function() {
      this.$prompt('请输入书名', '搜索小说', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        center: true,
        showClose: false
      }).then(({value}) => {
        this.$emit('searchBook', value);
      });

    }
  }
}
</script>
