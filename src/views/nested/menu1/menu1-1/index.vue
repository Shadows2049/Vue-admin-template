<template>
  <div class="app-container" style="padding: 30px">
    <el-alert :closable="false" title="menu 1-1" type="success">
      <router-view />
    </el-alert>
  </div>
</template>
<style>
.app-container {
  background-color: #9ab4b4;
}
</style>
