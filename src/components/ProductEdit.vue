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
        <button class="button is-success" @click="updateProduct">UPDATE</button>
    </div>
</template>

<script>
// import axios
import axios from "axios";

export default{
    name: "ProductEdit",
    data(){
        return {
            productName: "",
            productPrice: "",
        }
    },

    created: function (){
        this.getProductById()
    },

    methods: {
        // Get Product By Id
        async getProductById(){
            try {
                const response = await axios.get("link API")

                this.productName = response.data.response[0].product_name
                this.productPrice = response.data.response[0].product_price
            } catch (err) {
                console.log(err)
            }
        },

        // Update product
        async updateProduct(){
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