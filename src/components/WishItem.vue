<template>
    <div class="item" v-bind:class="{'item--completed':item.completed}">
        <input type="checkbox" class="item__checkbox" v-on:change="markComplete">
        <p class="item__title">{{item.title}}</p>
        <button class="item__delete" @click="delItem(item.id)">x</button>
    </div>
</template>

<script>
export default {
    name: "WishItem",
    props: ['item'],
    methods: {
        markComplete() {
            this.item.completed = !this.item.completed;
        },

        delItem(id) {
            this.$emit('del-item', id)
        }
    }
}
</script>

<style scoped>
    .item {
        display: flex;
        flex-direction: row;
        align-items: center;
        background: #f3f3f3;
    }

    .item:hover,
    .item:focus {
        background: #ffffff;
    }

    .item:hover > .item__delete,
    .item:focus > .item__delete {
        background: #e43434;
    }

    .is-completed .item__title {
        text-decoration-line: line-through;
    }

    .item__checkbox {
        margin: 0;
        padding: 0;
        margin-left: 20px;
    }

    .item__title {
        margin: 0;
        padding: 0;
        text-transform: capitalize;
        margin-left: 10px;
    }

    .item__delete {
        cursor: pointer;
        background: #ca2828;
        border: none;
        font-size: 1.3em;
        width: auto;
        height: 100%;
        margin-left: auto;
        color: #fff;
        padding: 15px 20px;
    }
</style>