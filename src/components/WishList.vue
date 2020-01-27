<template>
    <div>
        <div v-bind:key="item.id" v-for="item in wishlist" class="wishlist">
            <WishItem v-bind:item="item" v-on:del-item="$emit('del-item', item.id)" />
        </div>
    </div>
</template>

<script>
import WishItem from './WishItem';

export default {
    name: "WishList",
    components: {
        WishItem
    },
    props: ["wishlist"]
}
</script>

<style scoped>

</style>