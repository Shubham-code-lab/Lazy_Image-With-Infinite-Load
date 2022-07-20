<template>
  <div>
        <div class="container">
            <div v-for="(restaurantDetail, index) in restaurantsDetail" :key="restaurantDetail.id"  class="sub-container sub-container-first" :ref="'container'+index" @mouseover="containerHover(index)" @mouseout="containerNormal(index)">
                <div class="image-holder">
                    <img class="image-adjust" alt="Restaurant Card" :data-src="restaurantDetail.image" loading="lazy">
                    <div v-if="restaurantDetail" class="promoted">
                        <p>promoted</p>
                    </div>
                    <div class="discount">
                        <h4>{{restaurantDetail.discount}}% OFF</h4>
                    </div>
                    <div class="distance">
                        <h4>{{restaurantDetail.timeToReach}} min</h4>
                    </div>
                </div>
                <div>
                    <div class="name-rating">
                        <b>{{restaurantDetail.name}}</b>
                        <div>
                            <span>{{restaurantDetail.rating}}</span>
                        </div>
                    </div>
                    <div class="food-pricing">
                        <p>{{restaurantDetail.foodType}}</p>
                        <span>₹{{restaurantDetail.foodPricing}} for one</span>
                    </div>
                </div>
                <hr>
                <div class="trust">
                    <div class="trust-img-first">
                        <img class="first-img" alt="image" src="https://b.zmtcdn.com/data/o2_assets/4bf016f32f05d26242cea342f30d47a31595763089.png?output-format=webp" loading="lazy">
                    </div>
                    <p class="trust-text">{{restaurantDetail.numberOfOrders}}+ orders placed from here recently</p>
                    <div class="trust-img-second">
                        <img class="second-img" alt="image" src="https://b.zmtcdn.com/data/o2_assets/0b07ef18234c6fdf9365ad1c274ae0631612687510.png?output-format=webp" loading="lazy">
                    </div>
                </div>
            </div>   
         </div>
    </div>
</template>

<script>
export default {
    props:['restaurantsDetail','onScreenParentElement'],
    mounted() {
        
    },
  data() {
        return {
            activeElement: null,
        }
    },
    methods: {
        containerHover(elementNumber) {
            // console.log(this.$refs["container"+elementNumber][0]);  //v-for index passed to dynamic value ref 
            for(let i = 0;i<3;i++){
                this.$refs["container"+i][0].style.width = "26%";
            }
            this.activeElement = this.$refs["container"+elementNumber][0];
            // console.log(this.activeElement);
            this.activeElement.style.width = "32%";
            this.activeElement.style.boxShadow = "rgba(0, 0, 0, 0.35) 0px 5px 15px";
            this.activeElement.style.borderRadius = "5%";
        },
        containerNormal() {
            for(let i = 0;i<3;i++){
                this.$refs["container"+i][0].style.width = "28%";
            }
            this.activeElement.style.boxShadow = null;
            this.activeElement.style.borderRadius = null;
            // console.log(this.activeElement);
        }
    },
    watch:{
        onScreenParentElement(newElement){
            console.log("ImageComponent");
            console.log(newElement.firstChild.firstChild.children);  //3 image comp of one row
            let rowImages = newElement.firstChild.firstChild.children;
            for(let i= 0;i<rowImages.length;i++){
                console.log("hii",rowImages[i]);    //subcontainer
                let imgElement = rowImages[i].firstChild.firstChild;
                // console.log(imgElement.getAttribute('data-src'));
                imgElement.src = imgElement.getAttribute('data-src');
                // imgElement.removeAttribute("data-src")
            }
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
    display: flex;
    flex-wrap: wrap;
    gap: 1%;
    justify-content: center;
    width: 100%;
    height: 400px;
}

.sub-container {
    /* margin-top: 50px; */
    height: 100%;
    min-width: 250px;
    width: 30%;
    padding: 1%;
    transition: width 1s, border-radius 1s, box-shadow 1s;
}

.image-holder {
    height: 70%;
    width: 100%;
    position: relative;
}

.image-adjust {
    height: 100%;
    width: 100%;
    object-fit: cover;
    border-radius: 2%;
    /* transform: scale(1);
    transition: transform 1s; */
}

.promoted,
.discount,
.distance {
    position: absolute;
}

.promoted {
    top: 2%;
    left: 2%;
    padding: 0% 1%;
    border-radius: 10%;
    background-color: rgba(48, 48, 48, 0.814);
    color: rgb(135, 130, 130);
}

.discount {
    bottom: 3%;
    background-color: blue;
    color: white;
    padding-right: 1%;
}

.distance {
    border-radius: 15%;
    padding: 0% 1%;
    background-color: gray;
    bottom: 3%;
    right: 2%;
}

.name-rating,
.food-pricing {
    margin: 2% 0%;
    display: flex;
}

.food-pricing>p,
.name-rating>b {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}

.name-rating>b {
    width: 85%;
    font-size: larger;
}

.name-rating>div {
    align-self: center;
    height: 100%;
    background-color: green;
    padding: 0% 3%;
    border-radius: 10%;
}

.food-pricing>span {
    margin-left: auto;
}

.trust {
    display: flex;
    justify-content: flex-start;
    width: 100%;
}

.trust-img-second {
    margin-left: auto;
    width: 20%;
}

.trust-img-first {
    width: 8%;
    padding: 2%;
}

.first-img,
.second-img {
    object-fit: scale-down;
    /* width: 50%; */
}

.trust-img-second img {
    width: 100%;
    margin-top: 10%;
}

.trust-img-first img {
    width: 100%;
}

.trust-text {
    font-size: smaller;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    height: 100%;
    align-self: center;
    width: 60%;
}
</style>
