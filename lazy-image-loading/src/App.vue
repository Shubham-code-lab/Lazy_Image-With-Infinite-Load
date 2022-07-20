<template>
  <h1>dd</h1>
  <h1>dd</h1>
  <h1>dd</h1>
  <h1>dd</h1>
  <h1>dd</h1>
  <h1>dd</h1>
  <h1>dd</h1>
  <h1>dd</h1>
  <h1>dd</h1>
  <h1>dd</h1>
  <h1>dd</h1>
  <h1>dd</h1>
  <h1>dd</h1>
  <h1>dd</h1>
  <h1>dd</h1>
  <h1>dd</h1>
  <h1>dd</h1>
  <h1>dd</h1>
  <h1>dd</h1>
  <h1>dd</h1>
  <h1>dd</h1>
  <h1>dd</h1>
  <h1>dd</h1>
  <h1>dd</h1>
  <div>
        <!-- loadItemSet is 2 so itemSet is 1,2 -->
    <div v-for="itemSet in loadItemSet" :key="itemSet" :ref="'parentContainer' + itemSet" class="parent-container">
      <img-component :restaurantsDetail='restaurantsDetail' :onScreenParentElement="onScreenParentElement"></img-component>  
    </div>
  </div>
</template>

<script>
import ImgComponent from './components/ImgComponent.vue'

export default {
  name: 'App',
  components: {
    ImgComponent
  },
  mounted() {
    const option = {
      root: null,
      threshold: 0,
      // rootMargin: "150px"
    }
    const observer = new IntersectionObserver((entries, observer)=>{
      entries.forEach(entry=>{
      if(!entry.isIntersecting){
         console.log("not on screen");
         console.log(entry.target);
      } else{
        this.onScreenParentElement = entry.target; 
      this.loadItemSet += 2;   //for refs
      console.log("on screen item",this.loadItemSet, this.$refs,entry.target,entries);
      this.$nextTick(() => {                          //wait to get new render data
         addMoreItems(this.loadItemSet,this.$refs);
      });
      
      console.log("unobserve");
      console.log(this.onScreenParentElement);
      observer.unobserve(entry.target);
      }    
    });
    }, option);
   
    function addMoreItems(newContainers, refs){
        console.log("addMoreItems",newContainers,refs);
        for(let itemSet=newContainers-1;itemSet<=newContainers;itemSet++){
              console.log(itemSet);
              console.log(refs);
              console.log(document.querySelectorAll('.parent-container'));
              observer.observe(refs["parentContainer" + itemSet][0]);
        }
    }
     addMoreItems(this.loadItemSet,this.$refs);
  },
  data() {
    return {
      onScreenParentElement: null,
      loadItemSet: 2,
      restaurantsDetail:[{
        id: 1,
        name:'Shri Ganesh Nashta Centre',
        foodType:'Biryani, North Indian',
        image:'https://b.zmtcdn.com/data/pictures/8/19054158/1398bcdd22330367e9768f0dc9b040cd_o2_featured_v2.jpg?output-format=webp',
        foodPricing:150,
        rating:3.5,
        discount:20,
        timeToReach:25,
        promoted:true,
        numberOfOrders:"3000+ orders placed from here recently",
      },
      {
        id: 2,
        name:'Shri Ganesh Nashta Centre',
        foodType:'Biryani, North Indian',
        image:'https://b.zmtcdn.com/data/pictures/3/19241443/06753e3d0a4bf12acb673af12acd47d3_o2_featured_v2.jpg?output-format=webp',
        foodPricing:150,
        rating:3.5,
        discount:20,
        timeToReach:25,
        promoted:true,
        numberOfOrders:"3000+ orders placed from here recently",
      },
      {
        id: 3,
        name:'Shri Ganesh Nashta Centre',
        foodType:'Biryani, North Indian',
        image:'https://b.zmtcdn.com/data/pictures/6/19711626/252a39792b46c72bec7832a17261ce78_o2_featured_v2.jpg',
        foodPricing:150,
        rating:3.5,
        discount:20,
        timeToReach:25,
        promoted:true,
        numberOfOrders:"3000+ orders placed from here recently",
      }]
    }
  },
}
</script>

<style scoped>

.parent-container {
  /* height: 1000px; */
    width: 75%;
    margin: 40px auto;
}
@media only screen and (max-width: 1020px) {
  .parent-container{
    height: 800px;
  }}
  @media only screen and (max-width: 671px) {
  .parent-container{
    height: 1200px;
  }
  }
    

</style>
