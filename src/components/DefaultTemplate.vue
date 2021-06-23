<template>
  <div id="modal">
    <div class="st-product">
      <div>
        <div class="st-row">

          <div class="st-col-md-3 st-products" v-for="item in results" :key="item.id">
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
#Modal .st-product{
  display: flex;
  flex-wrap: wrap;
  width: 100%;
}

.st-row {
  margin-right: -15px;
  margin-left: -15px;
  display: flex;
  flex-wrap: wrap;
  box-sizing: border-box;
}

.st-col-md-3{
  position: relative;
  padding-right: 15px;
  padding-left: 15px;
  box-sizing: border-box;
  width: 33.33%;
}

.loadMore{
  padding: 10px 20px;
  border:none;
}

.loadMore:hover{
  cursor: pointer;
}
</style>
