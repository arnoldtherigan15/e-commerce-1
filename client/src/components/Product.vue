<template>
    <div class="container">
        <!-- Vegetable -->
        <div v-if="filterTag.isVegetable">
        <div style="display:flex;">
            <div class="mt-1">
                <img src="https://firebasestorage.googleapis.com/v0/b/project-2059615900628317391.appspot.com/o/category-icon-new%2F1530182713018_Vegetables-min.png?alt=media&token=e12445f7-57fb-45ec-bf5a-87993ddec8a5" alt="category" style="width:50px;">
            </div>
            <div class="ml-2 mt-3">
                <p style="color:black;">Vegetables</p>
            </div>
        </div>
        <div class="mb-4" style="display:flex; flex-wrap:wrap; justify-content:center;">
            <div v-for="vegetable in vegetables" :key=vegetable._id class="card mx-2 my-2" style="width:23%;">
            <img class="ribbon" src="../../public/ribbon3.png" alt="ribbon">
            <p class="text-ribbon">Organic</p>
                <img :src=vegetable.image class="card-img-top zoom" alt="product" style="height:250px; object-fit: cover; cursor:pointer;" @click="getdetail(vegetable._id)">
                <div class="card-body">
                    <h5 class="card-title">{{ vegetable.name }}</h5>
                    <p class="card-text">Rp. {{ vegetable.price }}/kg</p>
                    <a @click.prevent="addtoCart(vegetable._id)" style="color:white; cursor:pointer;" class="btn btn-success form-control">beli</a>
                </div>
            </div>
        </div>
        </div>
        <!-- Fruit -->
        <div v-if="filterTag.isFruit">
            <div style="display:flex;">
                <div class="mt-1">
                    <img src="https://firebasestorage.googleapis.com/v0/b/project-2059615900628317391.appspot.com/o/category-icon-new%2F1530181378402_SAYURICON-buah-min.png?alt=media&token=9551f990-8bd8-4791-87cc-1f8b7f61a3cf" alt="category" style="width:50px;">
                </div>
                <div class="ml-2 mt-3">
                    <p style="color:black;">Fruits</p>
                </div>
            </div>
            <div class="mb-4" style="display:flex; flex-wrap:wrap; justify-content:center;">
                <div v-for="fruit in fruits" :key=fruit._id class="card mx-2 my-2" style="width:23%;">
                    <img class="ribbon" src="../../public/ribbon3.png" alt="ribbon">
                    <p class="text-ribbon">Organic</p>
                    <img :src=fruit.image class="card-img-top zoom" alt="product" style="height:250px; object-fit: cover; cursor:pointer;" @click="getdetail(fruit._id)">
                    <div class="card-body">
                        <h5 class="card-title">{{ fruit.name }}</h5>
                        <p class="card-text">Rp. {{ fruit.price }}/kg</p>
                        <a @click.prevent="addtoCart(fruit._id)" style="color:white; cursor:pointer;" class="btn btn-success form-control">beli</a>
                    </div>
                </div>
            </div>
        </div>
        <!-- protein-->
        <div v-if="filterTag.isProtein">
            <div style="display:flex;">
                <div class="mt-1">
                    <img src="https://firebasestorage.googleapis.com/v0/b/project-2059615900628317391.appspot.com/o/category-icon-new%2F1560915523722_sayurbox%20icon%20package%20OPS-04.png?alt=media" alt="category" style="width:50px;">
                </div>
                <div class="ml-2 mt-3">
                    <p style="color:black;">Protein</p>
                </div>
            </div>
            <div class="mb-4" style="display:flex; flex-wrap:wrap; justify-content:center;">
                <div v-for="protein in proteins" :key=protein._id class="card mx-2 my-2" style="width:23%;">
                    <img class="ribbon" src="../../public/ribbon3.png" alt="ribbon">
                    <p class="text-ribbon">Organic</p>
                    <img :src=protein.image class="card-img-top zoom" alt="product" style="height:250px; object-fit: cover; cursor:pointer;" @click="getdetail(protein._id)">
                    <div class="card-body">
                        <h5 class="card-title">{{ protein.name }}</h5>
                        <p class="card-text">Rp. {{ protein.price }}/kg</p>
                        <a @click.prevent="addtoCart(protein._id)" style="color:white; cursor:pointer;" class="btn btn-success form-control">beli</a>
                    </div>
                </div>
            </div>
        </div>
        <!-- grain-->
        <div v-if="filterTag.isGrain">
            <div style="display:flex;">
                <div class="mt-1">
                    <img src="https://storage.googleapis.com/dev-sayurbox.appspot.com/sku-lg/1572497347275_scale_500x500_85_color_not_blur_oxl.jpg" alt="category" style="width:50px;">
                </div>
                <div class="ml-2 mt-3">
                    <p style="color:black;">Grain</p>
                </div>
            </div>
            <div class="mb-4" style="display:flex; flex-wrap:wrap; justify-content:center;">
                <div v-for="grain in grains" :key=grain._id class="card mx-2 my-2" style="width:23%;">
                    <img class="ribbon" src="../../public/ribbon3.png" alt="ribbon">
                    <p class="text-ribbon">Organic</p>
                    <img :src=grain.image class="card-img-top zoom" alt="product" style="height:250px; object-fit: cover; cursor:pointer;" @click="getdetail(grain._id)">
                    <div class="card-body">
                        <h5 class="card-title">{{ grain.name }}</h5>
                        <p class="card-text">Rp. {{ grain.price }}/kg</p>
                        <!-- <a href="" class="btn btn-success form-control">beli</a> -->
                        <a @click.prevent="addtoCart(grain._id)" style="color:white; cursor:pointer;" class="btn btn-success form-control">beli</a>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { mapState, mapActions } from 'vuex'
import Swal from 'sweetalert2'

export default {
  name: 'Product',
  computed: {
    ...mapState([
      'fruits', 'vegetables', 'proteins', 'grains', 'filterTag', 'carts'
    ])
  },
  methods: {
    ...mapActions([
      'getDetailProduct', 'addCart', 'getCart'
    ]),
    getdetail (id) {
      this.getDetailProduct(id)
    },
    setCartAnim (param) {
      // this.IS_CART(param)
      this.$store.commit('IS_CART', param)
    },
    addtoCart (id) {
      this.setCartAnim(true)
      if (localStorage.getItem('token')) {
        this.addCart(id)
          .then(_ => {
            this.getCart()
            this.setCartAnim(false)
          })
          .catch(err => {
            console.log(err)
            this.setCartAnim(false)
            Swal.fire('errorr', 'internal server error', 'error')
          })
      } else {
          this.setCartAnim(false)
        this.$router.push('/user/login')
      }
    }
  }
}
</script>

<style scoped>
.ribbon {
    position: absolute;
    width: 40%;
    height: 40;
    top: -2%;
    left: 64%;
    z-index: 2;
}
.text-ribbon {
    position: absolute;
    top: -2%;
    left: 85%;
    transform-origin: 0 0;
    transform: rotate(46deg);
    color: white;
    z-index: 2;
}

.zoom:hover {
    filter:drop-shadow(8px 8px 10px #28a745);
}
</style>
