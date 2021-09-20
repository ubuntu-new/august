<template>
<!-- Start Cart Area -->
<section class="cart-area  backgroundWhite ">
    <div class="container desktopiza">
        <form>
            <div class="row ">
                <div class="col-lg-9 col-sm-12 checkoutLeftInner backgroundGray">
                    <div class="cart-table table-responsive">
                        <table class="table table-bordered webertela">
                            <thead>
                                <tr>
                                    <th>&nbsp;</th>
                                    <th scope="col">{{$t('cartItems.product')}}</th>
                                    <th scope="col">&nbsp;</th>
                                    <th scope="col">{{$t('cartItems.quantity')}}</th>
                                    <th scope="col">{{$t('cartItems.comment')}}</th>
                                    <!-- <th scope="col">Unit Price</th> -->
                                    <th scope="col">&nbsp;</th>
                                </tr>
                            </thead>

                            <tbody v-if="cart.length > 0">

                                <tr v-for="(cart, i) in cart" :key="i">
                                    <td>
                                        <a href="javascript:void(0)" @click="removeItemFromCart(cart.id)" class="remove">
                                            <img src="img/group-6.png" srcset="img/group-6@2x.png 2x,
                                                        img/group-6@3x.png 3x" class="Group-6">
                                        </a>
                                    </td>
                                    <td class="product-thumbnail">

                                        <a href="#">
                                            <img :src="`http://august.webertela.online/backend/web/images/store/${cart.image}`" :alt="cart.name" />
                                        </a>
                                    </td>

                                    <td class="product-name">
                                        <nuxt-link :to="`/products-details/${cart.id}`">
                                            {{cart.name}}
                                        </nuxt-link>
                                        <!-- <ul>
                                                    <li>Crust: <strong>Thin</strong></li>
                                                    <li>Some: <strong>ingridients</strong></li>
                                                </ul> -->
                                    </td>

                                    <td class="product-quantity">
                                        <div class="input-counter">
                                            <span @click="onDecrement(cart.id, cart.quantity)" class="minus-btn"><i class="fas fa-minus"></i></span>
                                            {{cart.quantity}}
                                            <span @click="onIncrement(cart.id)" class="plus-btn"><i class="fas fa-plus"></i></span>
                                        </div>
                                    </td>

                                    <td class="product-comment">
                                        <div class="input-counter">
                                            <br>
                                            <textarea v-model="message[i]" placeholder=" $t('cartItems.writeComment') ">></textarea>
                                        </div>
                                    </td>

                                    <!-- <td class="product-price">
                                        <span class="unit-amount">${{cart.price}}</span>
                                    </td> -->

                                    <td class="product-subtotal">
                                        <span class="subtotal-amount">${{cart.price * cart.quantity}}</span>

                                    </td>
                                </tr>

                            </tbody>
                        </table>
                    </div>
                </div>
                <div class="col-lg-3 col-sm-12 checkoutRightInner short">
                    <div class="racxa">
                        <div class="cart-table table-responsive">
                            <table class="table table-bordered webertela">
                                <thead>
                                    <tr>
                                        <th scope="col">{{$t('cartItems.details')}}</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>{{$t('cartItems.fullPrice')}} <span style="float:right"><b>{{parseFloat(cartTotal + 10).toFixed(2)}} ₾</b></span></td>
                                    </tr>
                                    <!-- <nuxt-link to="/checkout" class="btn btn-checkout">Buy</nuxt-link> -->
                                    <span @click="sendStep(2)" class="btn btn-checkout">{{$t('buy')}}</span>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>
        </form>
    </div>

    <div class="container mobiluriza">
        <form>
            <div class="row backgroundGray">
                <div class="col-sm-12 checkoutLeftInner ">
                    <div class="cartTitleMobile webertela">
                        <h5>Product</h5>
                    </div>
                </div>
                <div class="col-sm-12">
                    <ul v-if="cart.length > 0">
                        <li v-for="(cart, i) in cart" :key="i">
                            <div class="row remove">
                                <div class="col-12">
                                    <a href="javascript:void(0)" @click="removeItemFromCart(cart.id)" class="">
                                        <img src="img/group-6.png" class="removeImg">
                                    </a>
                                    <img :src="`http://august.webertela.online/backend/web/images/store/${cart.image}`" :alt="cart.name" class="cartItemImage" />
                                    <nuxt-link :to="`/products-details/${cart.id}`" class="cartName">
                                        {{cart.name}}
                                    </nuxt-link>
                                </div>
                            </div>
                            <div class="row">
                                <div class="col-7">
                                    <div class="product-quantity">
                                        <div class="input-counter">
                                            <span @click="onDecrement(cart.id, cart.quantity)" class="minus-btn"><i class="fas fa-minus"></i></span>
                                            {{cart.quantity}}
                                            <span @click="onIncrement(cart.id)" class="plus-btn"><i class="fas fa-plus"></i></span>
                                        </div>
                                    </div>
                                </div>
                                <div class="col-5">
                                    <span class="subtotal-amount">{{$t('cartItems.price')}}: {{cart.price * cart.quantity}} ₾ </span>
                                </div>
                                <div class="row">
                                    <div class="col-12">
                                        <div class="product-comment">
                                                <textarea v-model="message[i]" placeholder=" $t('cartItems.writeComment') "></textarea>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <hr>
                        </li>
                        
                    </ul>
                    
                </div>

                <!-- <div class="cart-table table-responsive">
                    <table class="table table-bordered webertela">

                        <tbody v-if="cart.length > 0">

                            <tr v-for="(cart, i) in cart" :key="i">
                                <td>
                                    <a href="javascript:void(0)" @click="removeItemFromCart(cart.id)" class="remove">
                                        <img src="img/group-6.png" srcset="img/group-6@2x.png 2x,
                                                        img/group-6@3x.png 3x" class="Group-6">
                                    </a>
                                </td>
                                <td class="product-thumbnail">

                                    <a href="#">
                                        <img :src="`http://august.webertela.online/backend/web/images/store/${cart.image}`" :alt="cart.name" />
                                    </a>
                                </td>

                                <td class="product-name">
                                    <nuxt-link :to="`/products-details/${cart.id}`">
                                        {{cart.name}}
                                    </nuxt-link>
                                </td>

                                <td class="product-quantity">
                                    <div class="input-counter">
                                        <span @click="onDecrement(cart.id, cart.quantity)" class="minus-btn"><i class="fas fa-minus"></i></span>
                                        {{cart.quantity}}
                                        <span @click="onIncrement(cart.id)" class="plus-btn"><i class="fas fa-plus"></i></span>
                                    </div>
                                </td>

                                <td class="product-comment">
                                    <div class="input-counter">
                                        <br>
                                        <textarea v-model="message[i]" placeholder="Write a comment"></textarea>
                                    </div>
                                </td>

                                <td class="product-subtotal">
                                    <span class="subtotal-amount">${{cart.price * cart.quantity}}</span>

                                </td>
                            </tr>

                        </tbody>
                    </table>
                </div> -->
            </div>
            <div class="row">
<div class="col-sm-12 checkoutRightInner short">
                <div class="racxa">
                    <div class="cart-table table-responsive">
                        <table class="table table-bordered webertela">
                            <thead>
                                <tr>
                                    <th scope="col">{{$t('cartItems.details')}}</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td>{{$t('cartItems.fullPrice')}}<span style="float:right"><b>${{parseFloat(cartTotal + 10).toFixed(2)}}</b></span></td>
                                </tr>
                                <span @click="sendStep(2)" class="btn btn-checkout">{{$t('cartItems.buy')}}</span>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
            </div>
            
        </form>
    </div>

</section>

<!-- End Cart Area -->
</template>

<script>
export default {
    computed: {
        cart() {
            return this.$store.getters.cart
        },
        cartTotal() {
            return this.$store.getters.totalAmount
        }
    },
    data() {
        return {
            message: [],
        }
    },
    methods: {
        sendStep(step) {
            this.$emit('onStep', step, this.message);
        },
        removeItemFromCart(id) {
            this.$store.dispatch('deleteCart', id)
        },
        onIncrement(id) {
            this.$store.dispatch('updateCart', {
                id,
                unit: 1,
                cart: this.cart
            })
        },
        onDecrement(id, quantity) {
            if (quantity > 1) {
                this.$store.dispatch('updateCart', {
                    id,
                    unit: -1,
                    cart: this.cart
                })
            } else {
                this.removeItemFromCart(id);
                this.$toast.warning("Item deleted!");
            }
        },
    }
}
</script>
