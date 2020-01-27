<template>
    <div>
        <form @submit="addItem">
            <div class="form__items">
                <input type="text" name="title" placeholder="Title" v-model="title">
                <input type="text" name="url" placeholder="Photo url" v-model="url">
            </div>
            <button type="submit">Submit</button>
        </form>
    </div>
</template>

<script>

// import uuid from 'uuid';

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
                // id: uuid.v4(),
                title: this.title,
                completed: false
            }
            this.$emit('add-item', newItem)
            this.title = ''
        }
    }
}
</script>

<style scoped>
    form {
        position: relative;
        display: flex;
        flex-direction: row;
        align-items: flex-end;
        flex-wrap: wrap;
        width: 100%;
        margin: 20px 0;
    }
    .form__items {
        display: flex;
        flex-direction: column;
    }

    input {
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
        width: 100px;
        font-weight: 500;
        padding: 5px 10px;
        border: none;
        border: solid 0 ;
        padding: 0 10px;
        margin-left: 80px;
        font-size: 1em;
        height: 60px;
    }

    button[type=submit]:focus,
    button[type=submit]:hover {
        background: #4DB6AC;
    }

    @media screen and (max-width: 600px) {
        form {
            flex-direction: column;
            align-items: center;
        }

        button[type=submit] {
            margin-left: 0;
            margin-top: 20px;
        }
    }

</style>