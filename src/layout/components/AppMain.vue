<template>
  <div>
    <particles />
    <section class="app-main">
      <transition name="fade-transform" mode="out-in">
        <router-view :key="key" />
      </transition>
    </section>
  </div>
</template>

<script>
import particles from '@/components/Particles/particles2.vue'
export default {
  name: 'AppMain',
  computed: {
    key() {
      return this.$route.path
    }
  },
  components: {
    particles
  }
}
</script>

<style scoped>
.app-main {
  /*50 = navbar  */
  min-height: calc(100vh+50px);
  width: 100%;
  position: absolute;

  overflow: hidden;
}
</style>

<style lang="scss">
// fix css style bug in open el-dialog
.el-popup-parent--hidden {
  .fixed-header {
    padding-right: 15px;
  }
}
#particles-js {
  position: absolute;
  margin-top: -50px;
  width: 100%;
  height: 100%;
  background-color: #9ab4b4;
  background-image: url('');
  background-repeat: no-repeat;
  background-size: contain;
  background-position: 50% 50%;
  z-index: -1;
}
</style>
