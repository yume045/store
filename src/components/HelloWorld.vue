<template>
  <div class="container">
    <div class="columns has-text-centered">
      <div class="column has-text-right">
        <img src="../assets/creative-logo-animations-2.gif" alt="" width="300px" height="auto">
      </div>
      <div class="column is-3"></div>
        <router-link to="/stock"><button class="button is-dark is-medium is-focused">STOCK</button></router-link>
    </div>
    <form action="">
      <div class="columns">
        <div class="column is-6 has-text-right">
          <p class="title is-6">ชื่อสินค้า</p><br>
          <p class="title is-6">จำนวนสินค้า</p><br>
          <p class="title is-6">ราคาสินค้า</p><br>
          <p class="title is-6">รูป</p><br>
        </div>
      <div class="column is-3 has-text-left">
          <p><input class="input" type="text" v-model="product.name"></p><br>
          <p><input class="input" type="text" v-model="product.total"></p><br>
          <p><input class="input" type="text" v-model="product.price"></p><br>
          <p><input class="input" type="text" v-model="product.img"></p><br>
        </div>
        <div class="column is-3"></div>
      </div>
      <div class="columns">
        <div class="column">
          <button class="button is-success is-medium is-focused" @click="addProduct()">ADD</button>
          <button type="reset"  class="button  is-dark is-medium is-focused">CLEAR</button><br>
          <div class="columes">
          <ul>
            <li class="col-3" v-for="product in productFire" :key="product['.key']">
                <a ><img :src="product.img" width="300" height="255"></a><br/>
                {{product.name}}<br/>
                <p class="price">{{product.price}} ฿</p>
                {{product.total}} left <br>
            </li>
          </ul>
        </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
import firebase from 'firebase'
var config = {
  apiKey: 'AIzaSyBulafJ8Y1niCM1s6SmGME-ccOCVWwqKj8',
  authDomain: 'store-2a382.firebaseapp.com',
  databaseURL: 'https://store-2a382.firebaseio.com',
  projectId: 'store-2a382',
  storageBucket: 'store-2a382.appspot.com',
  messagingSenderId: '767555506556'
}
var firebaseApp = firebase.initializeApp(config)
var db = firebaseApp.database()
var productRef = db.ref('products')
export default {
  name: 'HelloWorld',
  firebase: {
    productFire: productRef
  },
  data () {
    return {
      product: {
        name: '',
        total: '',
        price: '',
        img: ''
      }
    }
  },
  methods: {
    addProduct () {
      db.ref('/Products').push(this.product)
      this.product.name = ''
      this.product.total = ''
      this.product.price = ''
      this.product.img = ''
    },
    showStock () {
      db.ref('/Product')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
