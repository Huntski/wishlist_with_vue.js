<template>
    <header class="header">
        <h1>WishList</h1>
    </header>
</template>

<script>
export default {
    name: "Header"
}
</script>

<style scoped>
    .header {
        margin-top: 50px;
    }
    @media screen and (max-width: 600px){
        .header {
            text-align: center;
        }
    }
</style>