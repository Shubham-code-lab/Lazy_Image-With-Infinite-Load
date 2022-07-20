<template>
        <div class="image-holder"   >
            <!-- <div class="image-container"> -->
            <img class="image-adjust" alt="Restaurant Card" src="https://b.zmtcdn.com/data/pictures/3/19241443/06753e3d0a4bf12acb673af12acd47d3_o2_featured_v2.jpg?output-format=webp" loading="lazy">
            <!-- </div> -->
            <slot name="overImage"></slot>
        </div>
        <div>
            <div class="name-rating">
                <slot name="nameRating"></slot>
            </div>
            <div class="food-pricing">
                <slot name="foodPricing"></slot>
            </div>
        </div>
        <hr>
        <div class="trust">
            <div class="trust-img-first">
                <img class="first-img" alt="image" src="https://b.zmtcdn.com/data/o2_assets/4bf016f32f05d26242cea342f30d47a31595763089.png?output-format=webp" loading="lazy">
            </div>

            <p class="trust-text">3000+ orders placed from here recently</p>

            <div class="trust-img-second">
                <img class="second-img" alt="image" src="https://b.zmtcdn.com/data/o2_assets/0b07ef18234c6fdf9365ad1c274ae0631612687510.png?output-format=webp" loading="lazy">
            </div>
        </div>
</template>
<script>
export default {
    props:['restaurantDetail']
}
</script>
<style lang="">
    
</style>