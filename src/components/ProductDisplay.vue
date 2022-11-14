<template>
  <div class="bg"
    :class="{men:category == 'men\'s clothing', women:category == 'women\'s clothing', unavailable: category == 'unavailable'}">
  </div>
  <div class="product-box center">
    <div class="id">
      <p>Product ID : {{ product.id }}</p>
    </div>
    <div v-if="category != 'unavailable'">
      <div class="img-box">
        <img :src="product.image" alt="Product image" class="center">
      </div>
      <div class="details">
        <h3 class="product-title" :class="{men:category == 'men\'s clothing', women:category == 'women\'s clothing'}">
          {{ product.title }}</h3>
        <div class="sub-title">
          <p class="category">{{ category }}</p>
          <div class="rating" :class="{men:category == 'men\'s clothing', women:category == 'women\'s clothing'}">
            {{ product.rating.rate }}/5 <span>
              <div class="circle" :class="{checked: avgRating >= 1}"></div>
              <div class="circle" :class="{checked: avgRating >= 2}"></div>
              <div class="circle" :class="{checked: avgRating >= 3}"></div>
              <div class="circle" :class="{checked: avgRating >= 4}"></div>
              <div class="circle" :class="{checked: avgRating >= 5}"></div>
            </span></div>
        </div>

        <hr>
        <p class="description">{{ product.description}}</p>
        <hr>
        <h2 class="price" :class="{men:category == 'men\'s clothing', women:category == 'women\'s clothing'}">
          ${{ product.price }}</h2>
        <div class="buttons">
          <button class="buy" :class="{men:category == 'men\'s clothing', women:category == 'women\'s clothing'}">Buy
            now</button>
          <button @click="nextProduct" class="next-product"
            :class="{men:category == 'men\'s clothing', women:category == 'women\'s clothing'}">Next
            product</button>
        </div>
      </div>
    </div>

    <div v-if="category == 'unavailable'" class="unavailable-msg center">
      <p>This product is unavailable to show</p>
      <button class="unavailable-next-btn" @click="nextProduct">Next product</button>
    </div>
  </div>
</template>


<script>
  export default {
    data() {
      return {
        id: 1,
        product: 'null',
        category: null,
        avgRating: 0
      }
    },
    beforeCreate() {
      console.log('mounted')
      fetch('https://fakestoreapi.com/products/1')
        .then(res => res.json())
        .then(json => this.update(json))
    },
    methods: {
      update(json) {
        this.product = json
        this.avgRating = Math.round(json.rating.rate)
        if (json.category == 'men\'s clothing' || json.category == 'women\'s clothing') {
          this.category = json.category
        } else {
          this.category = 'unavailable'
        }
      },
      nextProduct() {
        this.id++
        fetch('https://fakestoreapi.com/products/' + this.id)
          .then(res => res.json())
          .then(json => this.update(json))
      }
    }
  }
</script>


<style>



  /*       #002772  #fde2ff #1e1e1e  #720060  #d6e6ff   #3f3f3f  #dcdcdc #ffffff        */
</style>