<template>
  <form class="row g-3">
    <div class="col-auto">
      <input type="email" class="form-control" id="search-field" v-model="searchPackageName" :placeholder="text">
    </div>
    <div class="col-auto">
      <button @click.prevent="searchPackage" class="btn btn-primary mb-3">{{ text }}</button>
    </div>
  </form>
</template>

<script>
export default {
  name: 'SearchPanel',
  props: {
    text: String
  },
  data() {
    return {
      packageList: '',
      searchPackageName: '',
      searchLists: [],

    }
  },
  methods: {
    searchPackage() {
      fetch(`https://data.jsdelivr.com/v1/packages/npm/${this.searchPackageName}`)
        .then(response => response.json())
        .then(data => {
          this.packageList = data;
          this.getPaginationLists(this.packageList.versions);
          this.$emit('packageName', this.packageList.name)
          this.getCountPagination;
        }).catch((error) => {
          console.log(error)
        });
    },
    getPaginationLists(list) {
      let array = list;
      let size = 10;
      let subarray = [];
      for (let i = 0; i < Math.ceil(array.length / size); i++) {
        subarray[i] = array.slice((i * size), (i * size) + size);
      }
      this.$emit('countPagination', subarray.length);
      this.$emit('list', subarray);
    }
  }

}
</script>

<style scoped lang="scss"></style>
