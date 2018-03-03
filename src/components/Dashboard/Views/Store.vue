
<template>
  <div class="row">

      <input type="text" v-model= "postBody.ProductName">   ProductName <br>
      <input type="text" v-model= "postBody.ProductPrice">   ProductPrice <br>
      <button @click="postPost()"> Create A product  </button>
      <li v-for="post in posts.data">
        <h8> ProductName:  {{ post.name}} Price:{{post.price}} Creation_Date:{{post.createdAt}} UpdatedAt:{{post.updatedAt}} SellerName:"Liza Charles" ProductId:{{post._id}}</h8>
      </li>


             <ul v-if="errors && errors.length">
             <li v-for="error of errors">
             {{error.message}}
             </li>
             </ul>

<br>
<br>
<br>
<br>

<br>
<br>
<br>
<br>
<br>
<br>

<input type="text" v-model= "postBody.updID" > Product_ID  <br>
<input type="text" v-model= "postBody.updatedName">   UpdateName <br>
<input type="text" v-model= "postBody.updatedPrice">   UpdatePrice <br>
<button @click="upd()" > Update Product  </button>
       <ul v-if="errors && errors.length">
       <li v-for="error of errors">
       {{error.message}}
       </li>
       </ul>


       <br>
       <br>
       <br>
       <br>
       <br>
       <br>


<input type="text" v-model= "postBody.delID" > ID  <br>
<button @click="del" > delete Product  </button>


 <ul v-if="errors && errors.length">
   <li v-for="error of errors">
     {{error.message}}
   </li>
 </ul>


<br><br><br><br><br><br>

<input type="text" v-model= "postBody.search" > Search For Product By Name <br>
<h8 v-for="post in posts.data" v-if="postBody.search === post.name" >
   ProductName:  {{ post.name}} Price:{{post.price}} Creation_Date:{{post.createdAt}} UpdatedAt:{{post.updatedAt}} SellerName:"Liza Charles" ProductId:{{post._id}}
 </h8>

 <br>
 <br>
 <br>


        <ul v-if="errors && errors.length">
        <li v-for="error of errors">
        {{error.message}}
        </li>
        </ul>

  </div>

  </div>






</template>
<script>
import axios from 'axios'
export default {
  data () {
    return {
      postBody: {
        ProductName: '',
        ProductPrice: '',
        updatedName: '',
        updatedPrice: '',
        delID: '',
        updID: '',
        searchID: '',
        search: ''
      },
      posts: [],
      errors: []
    }
  },
  mounted () {
    axios.get(`http://localhost:3000/api/product/getProducts`)
  .then(response => {
    // JSON responses are automatically parsed.
    this.posts = response.data
  })
  .catch(e => {
    this.errors.push(e)
  })
  },
  methods: {
    postPost () {
      axios.post(`http://localhost:3000/api/product/createProduct`, {
        name: this.postBody.ProductName,
        price: this.postBody.ProductPrice
      })
    .then(response => {
    })
    .catch(e => {
      this.errors.push(e)
    })
      window.location.reload()
    },
    upd () {
      axios.patch(`http://localhost:3000/api/Product/updateProduct` + '/' + this.postBody.updID, {
        name: this.postBody.updatedName,
        price: this.postBody.updatedPrice
      })
  .then(response => {
  })
  .catch(e => {
    this.errors.push(e)
  })
      window.location.reload()
    },
    del () {
      axios.delete('http://localhost:3000/api/product/deleteProduct' + '/' + this.postBody.delID)
.then(response => {
  console.log(response)
})
.catch(e => {
  this.errors.push(e)
})
      window.location.reload()
    },
    SearchForProduct () {
      axios.get('http://localhost:3000/api/product/getProduct' + '/' + this.postBody.searchID)
  .then(response => {
    console.log(response)
  })
  .catch(e => {
    this.errors.push(e)
  })
    }
  }
}
</script>
<style>

</style>
