<template>
  <nav class="nav">
    <div>
      <h2 style="padding-top: 20px; padding-left: 40px">My-Store</h2>

      <div>
         <button  class="log-btn"><router-link to="/login">Login</router-link> </button>
        <button  class="cart"><router-link to="/Cart">Cart ({{ cart }})</router-link> </button>
      
      </div>
    </div>
  </nav>

  <div v-for="item in itemList" :key="item.id" class="card">
     
    <img

      :src="item.image"
      class="card-img"
      style="width: 100%"
      alt="image"
    />

    <div class="product">
      <h5 style="font-size: 14px; margin-left: 12px; top: 10px">
        {{ item.title }}
      </h5>
      <!-- <p style="font-size: 15px; margin-left: 12px; margin-top: 6px">
        {{ item.description }}
      </p> -->
      <p
        style="
          font-size: 15px;
          margin-left: 12px;
          width: 55px;
          margin-top: 8px;
          background-color: #7042b9;
        "
      >
        ${{ item.price }}
      </p>
      <br />

     
       <button   style="
          font-size: 17px;
          margin-left: 20px;
          margin-bottom: 20px;
          background-color: #bdahg3e; ">
          <router-link to="/Details"> Buy </router-link> 
          </button>
      <button
        @click="addTocart()"
        style="font-size: 17px; margin-left: 50px; background-color: #bdaa3e"
      >
        Add to Cart
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      cart: 0,
      itemList: [],
    };
  },
  mounted() {
    fetch('https://fakestoreapi.com/products')
            .then(res=>res.json())
            .then(json=>this.itemList = json)
  },
  methods: {
    addTocart() {
      this.cart = this.cart + 1;
      fetch('https://fakestoreapi.com/carts/7',{
            method:"PUT",
            body:JSON.stringify(
                {
                    userId:3,
                    date:2019-12-10,
                    products:[{productId:1,quantity:3}]
                }
            )
        })
            .then(res=>res.json())
            .then(json=>this.productid = json)
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
html {
  overflow: scroll;
}
.nav {
  background-color: aqua;
  height: 60px;
}
.log-btn {
  color: white;
  background-color: rgb(90, 35, 90);
  padding: 2px 6px;
  font-size: 20px;
  position: relative;
  margin-left: 890px;
  top: -30px;
  display: inline-block;
}
.cart {
  padding: 2px 6px;
  font-size: 20px;
  position: relative;

  margin-left: 970px;
  top: -60px;
}
.card-img {
  height: 300px;
}
.card {
  position: relative;
  left: 50px;
  background-color: rgb(49 179 147 / 64%);
  width: 19rem;
  height: auto;
  top: 60px;
  border: rgb(37, 27, 27) solid 2px;
  margin-right: 24px;
  margin-bottom: 40px;
  border-color: black;
  border-radius: 10px rgb(87, 187, 137);
}
.product {
  background-color: rgb(110, 209, 188);
}
.app {
  top: 5%;
  margin-right: 22px;
}
h3 {
  margin: 40px 0 0;
}
ul {
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
</style>
