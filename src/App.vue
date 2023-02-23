<script setup lang="ts">
 import menuIcon from "../images/icon-menu.svg"
 import cart from "../images/icon-cart.svg"
 import avatar from "../images/image-avatar.png" 
 import iconClose from "../images/icon-close.svg"
 import ImageCarousel from "./components/ImageCarousel.vue"
    import Product from "./components/Product.vue"
    import product1 from "../images/image-product-1.jpg"
    import deleteIcon from "../images/icon-delete.svg"
import { onMounted, ref, watch } from "vue"
    let menu = $ref(false)
    let dialog = $ref(null)
    let cartUser = $ref(false)
    let cartAmount = $ref(0)
    function dialogs() {
        menu = !menu
        if(!dialog.open) {
            dialog.showModal()
        } 
    }
    onMounted(() => {
        
        console.log(dialog)
        
        // dialog.open()
    })
    function close() {
        dialog.close()
    }
    function addCart(q: number) {
        cartAmount += q
    }
    function removeCart() {
        cartAmount--
    }
    function removeItem() {
        cartAmount != 0 ? cartAmount-- : cartAmount = 0
    }
</script>

<template>
    <dialog class="sidebar relative left-0 w-3/4 h-full" ref="dialog">
        <div class="sidebar-content flex flex-col absolute top-20 gap-4 left-6 h-full bg-white">
            <a>Collections</a>
            <a>Men</a>
            <a>Woman</a>
            <a>About</a>
            <a>Contact</a>
            </div>
            <button @click="close" class="absolute left-2 top-2 p-4">
                <img :src="iconClose" alt="menu icon" class="lg:hidden max-h-max" />
            </button>
    </dialog>
    <header class="header flex flex-row gap-2 p-8">
        <div class="mt-2">
            <button @click="dialogs">
        <img :src="menuIcon" alt="menu icon" class="lg:hidden max-h-max" />
            </button>
       </div>
        <nav class="nav flex w-full ">
            <p class="logo mr-6">sneakers</p>
            <div class="gap-5 flex-row mt-1 hidden lg:flex">
            <a class="desktop-nav">Collections</a>
            <a class="desktop-nav">Men</a>
            <a class="desktop-nav">Woman</a>
            <a class="desktop-nav">About</a>
            <a class="desktop-nav">Contact</a>
            </div>
            <div class="flex justify-end w-full gap-4">
            <div class="relative">
            <img @click="cartUser = !cartUser" :src="cart" alt="cart icon" class="cart-icon-container h-5 w-5 lg:mt-2 lg:mr-2 relative" />
            <div class="absolute left-3 -top-1 circle flex justify-center items-center h-5 w-5" v-if="cartAmount > 0">
                <p class="text-center text-white">{{cartAmount}}</p>
</div>
                </div>
           
            
            <img :src="avatar" alt="avatar" class="h-5 w-5 lg:h-10 lg:w-10 avatar " />
            
            </div>
        </nav>
        
    </header>
    <div class="container pt-8 pl-2 pr-6 ">
    <div class="cart w-full lg:w-1/3 lg:right-0 h-56  mt-2 absolute z-10 bg-white overflow-hidden " v-if="cartUser">
        <h1 class="text-start cart-text">Cart</h1>
        <div class="h-[0.5px] mt-5 divider bg-gray-200 w-full" />
            <p class="empty mt-10" v-if="cartAmount == 0">Your cart is empty.</p>

        <div class="item-container h-full flex flex-col px-4 " v-if="cartAmount > 0">
              <div class="flex flex-row gap-2">
                <img class="h-10 h-10 mt-2" :src="product1" />
              
                <div class="flex flex-col w-full gap-1">

                    <p class="text-start text-container">Fall Limited Edition Sneakers</p>
                    <div class="flex flex-row w-full">
                    <p class="text-start  text-container mr-2">$125.00 x {{cartAmount}}</p>
                    <h2>${{cartAmount * 125}}.00</h2>
                    </div>
                    

                </div>
                 <div class="trash">
                    <img @click="removeItem" :src="deleteIcon" alt="delete" class="h-5 w-5 mt-4" />
                    </div>
                  </div>
           
                    <div class="basis-1">

            <button class="checkout p-4  text-white" v-if="cartAmount > 0">Checkout</button>
                    </div>

            </div>
   

         </div>

    </div>
    <main class="flex flex-col lg:flex-row">
   <section class="image-carousel lg:w-1/2 lg:p-8 ">
    <ImageCarousel />
   </section>
   <section class="product lg:pt-8 lg:w-1/2 lg:mt-16">
    <Product @add-to-cart="addCart" @remove-from-cart="removeCart" @open-cart="cartUser = !cartUser" />
    </section>
    </main>
</template>

<style scoped>
.cart-icon-container {
    cursor: pointer;
}
.cart-icon-container:hover {
}
.desktop-nav {
    font-size: 16px;
    font-family: Kumbh Sans;
    color: hsl(219, 9%, 45%);
    position: relative;
}
.avatar {
    cursor: pointer;
    position: relative;
}
.avatar:hover {
    border-radius: 100%;
    border: 3px solid hsl(26, 100%, 55%);
}
.desktop-nav:hover::after {
    content: '';
    position: absolute;
    bottom: -10px;
    left: 0;
    width: 100%;
    height: 2px;
    border: 1px solid hsl(26, 100%, 55%);
}
h2 {
    font-family: Kumbh Sans;
    font-weight: 700;
    font-size: 16px;
    color: hsl(220, 13%, 13%);
}
.checkout {
    background: hsl(26, 100%, 55%);
    border-radius: 10px;
    width: 100%;
    margin-top: 20px;
}
.circle {
    background: hsl(26, 100%, 55%);
    border-radius: 50px;
}
.empty, .text-container  {
    color:  hsl(219, 9%, 45%);
}
.cart-text {
    font-size: 20px;
    font-family: Kumbh Sans;
    font-weight: 700;
    color: hsl(220, 13%, 13%);
}
a {
    font-size: 16px;
    font-family: Kumbh Sans;
    font-weight: 700;
    color: hsl(220, 13%, 13%);
    cursor: pointer;
    position: relative;
    width: 100%;
    text-align: start;
}
a:hover::after {
    content: "";
    margin-top: 5px;
    border: 1px solid black;
    position: absolute;
    bottom: 0;
    left: 0;
    width: 80%;
}
    .logo {
    font-weight: 700;
    color: black;
    font-size: 20px;
    font-family: Kumbh Sans;
}
dialog {
    transition: all 0.3s ease-in-out;
    max-height: 100vh;
}
dialog:modal {
    position: absolute;
    margin: 0px;
    max-width: auto;
    max-height: auto;
    user-select: text;
    visibility: visible;
    overflow: auto;
}
.cart {
    max-width: 95%;
}
</style>


### Primary

- Orange: hsl(26, 100%, 55%)
- Pale orange: hsl(25, 100%, 94%)

### Neutral

- Very dark blue: hsl(220, 13%, 13%)
- Dark grayish blue: hsl(219, 9%, 45%)
- Grayish blue: hsl(220, 14%, 75%)
- Light grayish blue: hsl(223, 64%, 98%)
- White: hsl(0, 0%, 100%)
- Black (with 75% opacity for lightbox background): hsl(0, 0%, 0%)

## Typography

### Body Copy

- Font size (paragraph): 16px

### Font

- Family: [Kumbh Sans](https://fonts.google.com/specimen/Kumbh+Sans)
- Weights: 400, 700
