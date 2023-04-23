<template>
    <div v-if="isOpen" class="v-modal-shadow" @click.self="closeModal">
        <div class="v-modal">
            <div class="v-modal-close" @click="closeModal">&#10006;</div>
            <slot name="title">
                <h3 class="v-modal-title">Список файлов</h3>
            </slot>
            <slot name="body">
                <ul class="list-group">
                    <li v-for="item in listInfo" :key="item"
                        class="list-group-item d-flex p-2 justify-content-between align-items-center">
                        <div><span class="fs-6 fw-bold">Тип:</span> {{ item.type }}</div>
                        <div><span class="fs-6 fw-bold">Имя:</span> {{ item.name }}</div>
                    </li>
                </ul>
            </slot>
            <slot name="footer">
                <div class="v-modal-footer">
                    <button class="v-modal-footer__button" @click="closeModal">
                        Ок
                    </button>
                </div>
            </slot>
        </div>
    </div>
</template>

<script>
export default {
    name: "ModalWindow",
    props: {
        isOpen: Boolean,
        listInfo: Array,
    },
    data: function () {
        return {

        }
    },
    methods: {
        closeModal: function () {
            this.$emit('closeModal', false)
        }
    }
}
</script>

<style lang="scss">
.v-modal-shadow {
    position: absolute;
    top: 0;
    left: 0;
    min-height: 100%;
    width: 100%;
    background: rgba(0, 0, 0, 0.39);
    z-index: 1031;
    overflow: hidden;
}

.v-modal {
    background: #fff;
    border-radius: 8px;
    padding: 15px;
    min-width: 320px;
    max-width: 480px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);

    &-close {
        border-radius: 50%;
        color: #fff;
        background: #0d6efd;
        display: flex;
        align-items: center;
        justify-content: center;
        position: absolute;
        top: 7px;
        right: 7px;
        width: 30px;
        height: 30px;
        cursor: pointer;
    }

    &-title {
        color: #0d6efd;
    }

    &-footer {
        &__button {
            background-color: #0d6efd;
            color: #fff;
            border: none;
            text-align: center;
            padding: 8px;
            font-size: 17px;
            font-weight: 500;
            border-radius: 8px;
            min-width: 150px;
            margin-top: 20px;
        }
    }
}
</style>