<template>
  <div class="dashboard-container">
    <particles />
    <div class="dashboard-text">name: {{ name }}</div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import particles from '@/components/Particles/particles2.vue'
export default {
  name: 'Dashboard',
  computed: {
    ...mapGetters(['name'])
  },
  components: {
    particles
  }
}
</script>

<style lang="scss" scoped>
#particles-js {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: #e6ebee;
  background-image: url('');
  background-repeat: no-repeat;
  background-size: contain;
  background-position: 50% 50%;
}
.dashboard {
  &-container {
    background-color: #16858f;
  }
  &-text {
    font-size: 30px;
    line-height: 46px;
  }
}
/* ---- reset ---- */

canvas {
  display: block;
  vertical-align: bottom;
}
</style>
