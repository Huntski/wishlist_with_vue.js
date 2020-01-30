<template>
  <div id="app">
    <Header />
    <AddForm v-on:add-item="addItem" />
    <WishList
    v-bind:wishlist="wishlist"
    v-on:del-item="deleteItem"/>
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
      wishlist : [],
    }
  },
  methods: {
    deleteItem (item) {
      delete this.wishlist[this.wishlist.indexOf(item)]
      this.update()
    },

    addItem(item) {
      this.wishlist.push(item)
      this.update()
    },

    update() {
      let updatedList = []
      this.wishlist.forEach(v => {
        if (v != '' || v)
          updatedList.push(v)
      })
      this.wishlist = updatedList
      localStorage.setItem('wishlist', updatedList)
    }
  },
  created() {
    let wishlist = localStorage.getItem('wishlist')
    if (wishlist == null || wishlist == 'undefined') {
      localStorage.setItem('wishlist', [])
      wishlist = []
    }
    this.wishlist = wishlist.split(',')
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
