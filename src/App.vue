<script setup lang="ts"></script>

<template>
  <el-config-provider>
    <div id="app-container">
      <router-view></router-view>
    </div>
  </el-config-provider>
</template>

<style>
@import url('./assets/icons/iconfont.css');
@import url('./assets/fonts/fonts.css');
#app-container {
  width: 100vw;
  height: 100vh;
  background-color: #131422;
}
</style>
