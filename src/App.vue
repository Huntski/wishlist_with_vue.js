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
      jsonFile : 'assets/wishlist.json',
      wishlist : [],
      fs : require('fs')
    }
  },
  methods: {
    deleteItem (id) {
      let wishlist = this.getList()
      let updatedWishlist = []
      wishlist.forEach(item => {
        if (item.id !== id)
          updatedWishlist.push(item)
      })

      this.updateJson()
    },

    addItem(item) {
      this.wishlist.push(item)

      this.updateJson()
    },

    updateJson() {
      this.fs.writeFile(this.jsonFile, JSON.stringify(this.wishlist));
    },
  },
  created() {
    this.wishlist = JSON.parse(this.fs.readFileSync(this.jsonFile).toString());
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
