<script>
import axios from 'axios';

    export default { 
       // add code here
       data(){
        return{
            moods:["happy", "sad", "angry"],
            subject: '',
            entry: '',
            mood: '',
            statusMessage: ''
        }
       },
       
       computed:{
        baseUrl(){
            if (window.location.hostname=='localhost')
                return 'http://localhost:3000'
            else{
                const codespace_host = window.location.hostname.replace('5173','3000')
                return `https://${codespace_host}`; //backticks here
            }
        } 
       },

       methods:{
        addPost(){
            axios.get(`${this.baseUrl}/addPost`,{ //not single quotation mark! (') its backtick: (`))
                params: {
                    subject: this.subject,
                    entry: this.entry,
                    mood: this.mood

                }
            })
            .then(response=>{
                this.statusMessage = "Post added successfully";
                //clear fields
                this.subject= '';
                this.entry= '';
                this.mood= '';
            }
            ).catch(error=>{
                this.statusMessage = "Try again!";
            });
         }
        }
    }
</script>

<template>
    <div class="table m-2">
        <h3>Add a New Blog Post</h3>

        Subject: <input type='text' size='30' v-model='subject' required>
        <br>

        Entry: <br>
        <textarea name='entry' cols='80' rows='5' v-model='entry' required></textarea>
        <br>

        Mood:
        <!-- TODO: Build a dropdown list here for selecting the mood -->

        <!--required specifies a user must fill in a value before submitting form-->
        <select v-model="mood" required>
            <option v-for="mood in moods"> {{ mood }}</option>
        </select>

        <br>

        <br>
        <button @click="addPost()">Submit New Post</button>

        <p>{{ statusMessage }}</p>

        <hr> Click  <a><router-link to="/ViewPosts/">here</router-link></a>  to return to Main Page
       
    </div>
</template>

