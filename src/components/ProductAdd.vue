<template>
    <div>
        <div class="field">
            <label for="name" class="label">Product Name</label>
            <div class="control">
                <input type="text" class="input" placeholder="Product Name" v-model="productName">
            </div>
        </div>
    </div>

    <div class="field">
        <label for="price" class="label">Product Price</label>
        <div class="control">
            <input type="text" class="input" placeholder="Product Price" v-model="productPrice">
        </div>
    </div>

    <div class="control">
        <button class="button is-success" @click="saveProduct">SAVE</button>
    </div>
</template>

<script>
// import axios
import axios from "axios";

export default{
    name: "ProductAdd",
    data(){
        return {
            productName: "",
            productPrice: "",
        }
    },

    methods: {
        // Create New product
        async saveProduct(){
            try {
                await axios.post("link Api", {
                    product_name: this.productName,
                    product_price: this.productPrice,
                })

                this.productName = ""
                this.productPrice = ""
                this.$router.push("/")
            } catch (err) {
                console.log(err)
            }
        }
    }
}
</script>