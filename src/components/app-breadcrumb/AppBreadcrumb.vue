<template>
  <div class="breadcrumb">
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item v-for="(item, index) of breadcrumbData" :key="index" :to="{ path: item.path }">{{item.meta.title}}</el-breadcrumb-item>
    </el-breadcrumb>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Watch, Provide } from 'vue-property-decorator';

@Component({})
export default class AppBreadcrumb extends Vue {
  @Provide() private breadcrumbData: any[] = [];

  @Provide() private getRouteMatched():void {
    let matched = this.$route.matched.filter(item => item.name)
    this.breadcrumbData = this.$route.name === 'home'
      ? matched
      : [
        {
          name: 'home',
          path: '/home',
          meta: { title: 'Home' },
        }
      ].concat(matched);
  }
  mounted() {
    this.getRouteMatched();
  }

  @Watch('$route')
  aa() {
    this.getRouteMatched()
  }
}
</script>

<style lang="scss">
.breadcrumb{
  height: 50px;
  line-height: 50px;
  color: #fff!important;
  .el-breadcrumb{
    line-height: 50px;
    .el-breadcrumb__item{
      .el-breadcrumb__inner.is-link{
        color: #fff;
      }
    }
  }
}
</style>
