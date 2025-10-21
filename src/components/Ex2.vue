<script>
import { getEnabledCategories } from 'trace_events';

    export default { 
        // Add code in appropriate places
        data() {
            return {
                items: ['keyboard', 'mouse', 'iPhone', 'macbook', 'adapter'],
                itemAdded: ''
            }
            
        },

        methods:{
            addItem(){
                this.items.push(this.itemAdded);
                this.itemAdded = ''
            }
        }

    }
</script>

<template>

    <h2>Shopping Cart</h2>
    <!-- TODO: Add Code Here -->
     <ul>
        <li v-for="(item, index) in items" :key="index"> 
            {{ item }}
            <button v-on:click="items.splice(index, 1)">Delete!</button>
        </li>
     </ul>

     <!--@click is the shorthand-->
     <input type="text" v-model="itemAdded"> </input>
     <button v-on:click="addItem()" >Add!</button>
   
</template>
