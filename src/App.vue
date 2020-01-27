<template>
  <div id="app">
    <Header />
    <AddForm v-on:add-todo="addItem" />
    <WishList
    v-bind:wishlist="wishlist"
    v-on:del-wishlist="deleteWishItem"/>
  </div>
</template>

<script>
import Header from './components/layouts/Header';
import WishList from './components/WishList';
import AddForm from './components/AddForm';

export default {
  name: 'app',
  components: {
    WishList,
    Header,
    AddForm
  },
  data() {
    return {
      wishlist : [
        {
          id: 1,
          title: 'number 1',
          completed: false
        },
        {
          id: 2,
          title: 'number 3',
          completed: false
        },
        {
          id: 3,
          title: 'number 3',
          completed: false
        }
      ]
    }
  },
  methods: {
    deleteWishItem(id) {
      this.wishlist = this.wishlist.filter(item => item.id !== id);
    },

    addItem (item) {
      this.wishlist = [...this.wishlist, item];
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}

html,
body {
  font-family: Arial, sans-serif;
}

#app {
    max-width: 800px;
    margin: 0 auto;
    padding: 0 20px;
}
</style>
