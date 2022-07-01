<template>
  <div class="dashboard-container">
    <el-container class="ec">
      <el-aside width="40%">
        <el-row>
          <el-col :xs="24" :sm="24" :md="12" :lg="12" :xl="12"
            ><div class="grid-content bg-purple"></div
          ></el-col>
          <el-col :xs="24" :sm="24" :md="12" :lg="12" :xl="12"
            ><div class="grid-content bg-purple-light"></div
          ></el-col>
        </el-row>
        <el-row>
          <el-col :xs="24" :sm="24" :md="12" :lg="12" :xl="12"
            ><div class="grid-content bg-purple"></div
          ></el-col>
          <el-col :xs="24" :sm="24" :md="12" :lg="12" :xl="12"
            ><div class="grid-content bg-purple-light"></div
          ></el-col>
        </el-row>
        <el-row>
          <el-col :xs="24" :sm="24" :md="12" :lg="12" :xl="12"
            ><div class="grid-content bg-purple"></div
          ></el-col>
          <el-col :xs="24" :sm="24" :md="12" :lg="12" :xl="12"
            ><div class="grid-content bg-purple-light"></div
          ></el-col>
        </el-row>
      </el-aside>
      <el-container>
        <el-header height="50%">
          <el-row>
            <el-col :xs="24" :sm="12" :md="12" :lg="8" :xl="8"
              ><div class="grid-content bg-purple"></div
            ></el-col>
            <el-col :xs="24" :sm="12" :md="12" :lg="8" :xl="8"
              ><div class="grid-content bg-purple-light"></div>
            </el-col>
            <el-col :xs="24" :sm="12" :md="12" :lg="8" :xl="8"
              ><div class="grid-content bg-purple"></div>
            </el-col>
          </el-row>
          <div class="test">
            <el-rate
              class="er"
              v-model="value"
              :icon-classes="iconClasses"
              void-icon-class="el-icon-star-off"
              void-color="#377983"
              :colors="['#FFFFFF', '#F7BA2A', '#FF9900']"
            >
            </el-rate>
          </div>
        </el-header>
        <el-main height="50%"
          ><el-row>
            <el-col :xs="24" :sm="12" :md="12" :lg="8" :xl="8"
              ><div class="grid-content bg-purple"></div
            ></el-col>
            <el-col :xs="24" :sm="12" :md="12" :lg="8" :xl="8"
              ><div class="grid-content bg-purple-light"></div
            ></el-col>
            <el-col :xs="24" :sm="12" :md="12" :lg="8" :xl="8"
              ><div class="grid-content bg-purple"></div
            ></el-col> </el-row
        ></el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
export default {
  name: 'Dashboard',
  data() {
    return {
      value: null,
      iconClasses: ['el-icon-medal', 'el-icon-medal', 'el-icon-medal'] // 等同于 { 2: 'icon-rate-face-1', 4: { value: 'icon-rate-face-2', excluded: true }, 5: 'icon-rate-face-3' }
    }
  },
  computed: {
    ...mapGetters(['name'])
  }
}
</script>

<style lang="scss" scoped>
.dashboard {
  &-container {
    margin-top: 5%;
    padding: 15px;
    overflow: auto;
  }
}

.el-header,
.el-footer {
  background-color: transparentize($color: #b3c0d1, $amount: 0.38);

  color: #333;
  text-align: center;
  line-height: 60px;
}

.el-aside {
  background-color: transparentize($color: #d3dce6, $amount: 0.38);
  overflow: auto;
  height: 70vh;
  min-height: 500px;
  color: #333;
  text-align: center;
}

.el-main {
  background-color: transparentize($color: #1978d6, $amount: 0.88);

  color: #333;
  text-align: center;
  line-height: 160px;
}

.ec {
  border-width: 11px;

  -webkit-filter: drop-shadow(10px 10px 140px #377983);
}

.el-col {
  border-radius: 4px;
}
.bg-purple-dark {
  background: #99a9bf;
}
.bg-purple {
  background: #d3dce6;
}
.bg-purple-light {
  background: #e5e9f2;
}
.grid-content {
  border-radius: 14px;
  min-height: 50px;
  align-items: center;
  margin: 10px;
}
.er {
  padding: 5px;
}

.test {
  position: absolute;
  bottom: 51%;
  right: 1%;
  max-width: 250px;
  height: 35px;
}

::v-deep .el-rate__icon {
  font-size: 30px;
}
</style>
