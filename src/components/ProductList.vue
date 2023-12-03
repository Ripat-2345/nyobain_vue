<template>
    <div>
        <router-link :to="{name: 'Create'}" class="button is-success" style="margin-top:10px">Add New</router-link>
    </div>

    <table class="table is-striped is-bordered mt-3 is-fullwidth" style="margin: 10px auto;">
        <thead>
            <tr>
                <th>Product Name</th>
                <th>Product Price</th>
                <th class="has-text-centered">Actions</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="item in items" :key="item.product_id">
                <td>{{ item.product_name }}</td>
                <td>{{ item.product_price }}</td>
                <td class="has-text-centered">
                    <router-link :to="{name:'Edit', params: {id: item.product_id}}" class="button is-warning is-small">Edit</router-link>
                    <a class="button is-danger is-small" style="margin-left: 5px;" @click="deleteProduct(item.product.id)">Delete</a>
                </td>
            </tr>
        </tbody>
    </table>
</template>

<script>
import axios from 'axios';

export default {
    name: "ProductList",
    data(){
        return {
            items: []
        }
    },

    created(){
        this.getProducts();
    },

    methods:{
        // Get All Products
        async getProducts(){
            try{
                const response = await axios.get("link api")
                // this.items = response.data;
                this.items = response.data.response
            }catch(err){
                console.log(err)
            }
        },

        // Delete Product
        async deleteProduct(id){
            try{
                await axios.delete("link api")
                this.getProducts()
            }catch(err){
                console.log(err)
            }
        }
    }
}
</script>