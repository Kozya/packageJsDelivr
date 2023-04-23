<template>
  <div class="container app-container">
    <SearchPanel @countPagination="getcountPagination" @list="getPackageList" @packageName="getName" text="Поиск" />
    <PackageList :list="packageList" :pagination="countPagination" :name="packageName" />
    <AuthorInfo :author="packageName" />
  </div>
</template>

<script>
import SearchPanel from './components/SearchPanel.vue'
import PackageList from './components/PackageList.vue'
import AuthorInfo from './components/AuthorInfo.vue'

export default {
  name: 'App',
  components: {
    SearchPanel,
    PackageList,
    AuthorInfo,
  },
  data() {
    return {
      packageList: [],
      countPagination: 0,
      packageName: "",
    }
  },
  methods: {
    getPackageList(data) {
      this.packageList = data;
    },
    getcountPagination(data) {
      this.countPagination = data;
    },
    getName(data) {
      this.packageName = data;
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.app-container {
  padding-bottom: 100px;
}
</style>
