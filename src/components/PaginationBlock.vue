<template>
    <div class="pagination">
        <div :class="[{ 'active-tab': (active === item - 1) }, 'pagination-num']" v-for="item in count" :key="item"
            @click="changePage(item - 1)">{{ item }}</div>
    </div>
</template>

<script>
export default {
    props: {
        count: Number,
        active: Number,
    },
    data() {
        return {
            modalIsOpen: false,
            packageListInfo: [],
        }
    },
    methods: {
        changePage(num) {
            this.$emit('activeNum', num)
        }
    }
}
</script>

<style lang="scss">
.pagination {
    display: flex;
    margin-top: 20px;
    flex-wrap: wrap;

}

.pagination-num {
    width: 20px;
    height: 20px;
    border: 1px solid black;
    border-radius: 4px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-right: 5px;
    cursor: pointer;
    margin-bottom: 10px;
}

.pagination-num.active-tab {
    background-color: #0d6efd;
    color: white
}
</style>