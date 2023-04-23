<template>
    <div class="fixed-bottom footer d-flex justify-content-center align-items-center">
        <div v-if="author" class="container footer-container d-flex p-3 justify-content-between align-items-center">
            <p>Имя: {{ author }}</p>
            <p><a :href="'https://github.com/' + author">Домашняя страница автора</a></p>
        </div>
        <p v-else>введите название пакета и нажмите поиск</p>

    </div>
</template>

<script>
export default {
    props: {
        author: String,
    },
}
</script>

<style lang="scss">
.footer {
    height: 80px;
    background-color: #0d6efd;

    >p {
        color: #FFFFFF;
        margin: 0;
    }
}

.footer-container {
    p {
        color: #FFFFFF;
        margin-bottom: 0;

        a {
            color: #FFFFFF;
        }
    }
}
</style>