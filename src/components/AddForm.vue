<template>
    <div>
        <form @submit="addItem">
            <input type="text" name="title" placeholder="Title" v-model="title">
            <button type="submit">Add wish item</button>
        </form>
    </div>
</template>

<script>

import uuid from 'uuid';

export default {
    name: 'AddForm',
    data() {
        return {
            title: ''
        }
    },
    methods: {
        addItem (e) {
            e.preventDefault()
            if (this.title == '') return;
            const newItem = {
                id: uuid.v4(),
                title: this.title,
                completed: false
            }

            // Send to parent component
            this.$emit('add-todo', newItem)
            this.title = ''
        }
    }
}
</script>

<style scoped>
    form {
        display: flex;
        flex-direction: row;
        align-items: flex-end;
        width: 100%;
        margin: 20px 0;
    }

    input {
        max-width: 320px;
        border: none;
        border-bottom: solid 3px #00897B;
        height: 52px;
        font-size: 1.3em;
        transition: all .3s;
        outline: none;
        padding: 0 5px;
    }

    input::placeholder {
        transition: all .2s;
    }

    input:hover::placeholder,
    input:focus::placeholder {
        opacity: .3;
    }

    button[type=submit] {
        position: relative;
        cursor: pointer;
        background: #009688;
        color: #fff;
        max-width: 140px;
        font-weight: 500;
        padding: 5px 10px;
        border: none;
        border: solid 0 ;
        padding: 15px;
    }

    button[type=submit]:focus,
    button[type=submit]:hover {
        background: #4DB6AC;
    }

</style>