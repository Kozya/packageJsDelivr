<template>
    <ul class="list-group">
        <li v-for="(item, index) in list[activePage]" :key="item"
            @click="showPackageInfo(list[activePage][index].links.self)"
            class="list-group-item d-flex p-2 justify-content-between align-items-center">
            <div><span class="fs-6 fw-bold">Имя пакета:</span> {{ name }}</div>
            <div><span class="fs-6 fw-bold">версия:</span> {{ item.version }}</div>
        </li>
    </ul>
    <ModalWindow @closeModal="closeModal" :isOpen="modalIsOpen" :listInfo="packageListInfo" />
    <PaginationBlock @activeNum="getActivePage" :active="activePage" :count="pagination" v-if="list" />
    <div v-if="preloader" class="preloader">
        <img src="../assets/spiner.gif" alt="spiner">
    </div>
</template>

<script>
import ModalWindow from './ModalWindow.vue'
import PaginationBlock from './PaginationBlock.vue'
export default {
    components: {
        ModalWindow,
        PaginationBlock,
    },
    props: {
        list: Object,
        pagination: Number,
        name: String,
    },
    data() {
        return {
            modalIsOpen: false,
            packageListInfo: [],
            activePage: 0,
            paginationLists: [],
            preloader: false,
        }
    },
    methods: {
        openModal() {
            this.modalIsOpen = true;
        },
        closeModal() {
            this.modalIsOpen = false;
        },
        showPackageInfo(link) {
            this.preloader = true;
            fetch(`${link}`)
                .then(response => response.json())
                .then(data => {
                    this.packageListInfo = data.files;
                    this.preloader = false;
                    this.openModal()
                }).catch((error) => {
                    console.log(error)
                });
        },
        getActivePage(data) {
            this.activePage = data
        }
    }
}
</script>

<style lang="scss">
.list-group {
    li {
        cursor: pointer;
    }

    :hover {
        background-color: #dee2e6;
    }
}

.preloader {
    position: absolute;
    top: 0;
    left: 0;
    min-height: 100%;
    width: 100%;
    background: rgba(0, 0, 0, 0.39);
    z-index: 1031;
    overflow: hidden;

    img {
        width: 60px;
        margin: 30vh auto;
    }
}
</style>