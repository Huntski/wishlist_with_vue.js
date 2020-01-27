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
import axios from 'axios';

export default {
  name: 'app',
  components: {
    WishList,
    Header,
    AddForm
  },
  data() {
    return {
      // api : 'https://wieberanzijn.com/school/wishlist_api/',
      api : 'http://localhost/wishlist_api/',
      wishlist : [],
    }
  },
  methods: {
    deleteItem (id) {
      axios.post(this.api + '?r=remove', {
        'id' : id
      })

      let wishlist = this.getList()
      let newList = []
      wishlist.forEach(item => {
        if (item.id !== id)
          newList.push(item)
      })

      wishlist = newList
    },

    addItem(item) {

      let newItem = {
        title : item.title,
        url : item.url
      }

      axios.post(this.api + '?r=upload', newItem)

      this.wishlist.push(newItem)
    },
  },
  created() {
    axios.get(this.api)
      .then(res => this.wishlist = res.data)
      .catch()
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
