<template>
    <div class="content">
        <div v-bind:key="item.id" v-for="item in wishlist" class="wishlist">
            <WishItem v-bind:item="item" v-on:del-item="$emit('del-item', item.id)" />
        </div>
        <span v-if="!wishlist.length" class="wishlist__span">There are no items in your wishlist.</span>
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

    .content {
        margin-top: 50px;
    }
    .wishlist__span {
        font-size: 1.3em;
        margin-top: 190px;
    }

    @media screen and (max-width: 600px) {
        .content {
            text-align: center;
        }

        .wishlist__span {
            font-size: 1em;
        }
    }
</style>