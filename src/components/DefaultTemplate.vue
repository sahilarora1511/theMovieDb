<template>
  <div id="modal">
    <div class="st-product">
      <div>
        <div class="st-row">

          <div class="st-col-md-4 st-products" v-for="item in results" :key="item.id">
            <div class="st-card">
              <div class="st-product-element-top">
                <div class="st-img-container">
                  <a  class="st-loop-product">
                    <img :src="'http://image.tmdb.org/t/p/w400' + item.poster_path" />
                  </a>
                </div>
              </div>
              <div class="st-bottom-card">
                <div class="st-title-box">
                  <h3 class="st-product-title">
                    <a>
                      {{item.title}}
                    </a>
                  </h3>
                  <p>Original Language: <strong>{{item.original_language}}</strong></p>
                  <p>Original Title: <strong>{{item.original_title}}</strong></p>
                  <p>Release Date: <strong>{{item.release_date}}</strong></p>
                  <p>Popularity: <strong>{{item.popularity}}</strong></p>
                </div>

              </div>
            </div>
          </div>

        </div>
      </div>
    </div>
    <div id="footer"><button class="loadMore" @click="getNextPage" v-show="results.length>0 && page<totalPages">Load More</button></div>
  </div>
</template>

<script>
export default {
  name: 'DefaultTemplate',
  props:{
    results : Array,
    page: Number,
    totalPages: Number
  },
  methods:{
    getNextPage(){
      this.$emit('getMoreResults')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

#modal {
  position: relative;
  max-width: 100%;
  margin: 0 auto;
  padding: 10px 32px;
}

#modal .st-product{
  display: flex;
  flex-wrap: wrap;
  width: 100%;
}

.st-img-container {
  padding-bottom: 120%;
}

.st-img-container a img {
  vertical-align: top;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%,-50%);
  width: 100%;
  height: 100%;
  object-fit: contain;
}

a.st-loop-product {
  display: block;
  text-decoration: none;
  transition: all ease-out .3s;
}

.st-product-element-top {
  position: relative;
  display: block;
}

#modal .st-card {
  padding: 0 0;
  padding-top: 15px;
  margin-bottom: 25px;
}

.st-row {
  margin-right: -15px;
  margin-left: -15px;
  display: flex;
  flex-wrap: wrap;
  box-sizing: border-box;
}

.st-col-md-4{
  position: relative;
  box-sizing: border-box;
  width: 33.33%;
}

.loadMore{
  padding: 10px 20px;
  border:none;
  background-color: grey;
}

.loadMore:hover{
  cursor: pointer;
}

@media only screen and (max-width: 767px) {
  .st-col-md-4{
    width: 50%;
  }
}
</style>
