<template>
    <form @submit.prevent= "handleSubmit">

        <label>Email:</label>
        <input type="email" required v-model="email">

        <label>Password:</label>
        <input type ="password" required v-model="password">

        <div class="submit">
            <button @click="postUser()">Sign in</button>
        </div>

    </form>
</template>

<script>
import axios from 'axios';
import cookies from 'vue-cookies';
    export default {
        name: 'SigninForm',
        data() {
            return {
                email: '',
                password: '',         
                }
        },
        methods:{
            handleSubmit() {
                console.log('logged in')
            },
            postUser(){
                if (this.terms){
                    axios.request({
                        url:"http://127.0.0.1:5000/api/login",
                        method:"POST",
                        data:{
                            email: this.email,
                            password: this.password
                        }
                    }).then((response)=>{
                        cookies.set("token",response.data.loginToken);
                        this.$store.commit("updateUser",response.data);
                        this.$router.push("/");
                    }).catch(()=>{
                        console.log("something went wrong");
                    })
                }
            }
        }
        
    }
</script>

<style>
    form{
        max-width: 420px;
        margin: 30px auto;
        background:rgb(255, 255, 255);
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }
    label {
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6em;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }
    input {
        display: block;
        padding:10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color: #555;
    }
    input[type ="checkbox"] {
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0;
        position: relative;
        top: 2px;
    }
    button {
        background: cornflowerblue;
        border: 0;
        padding: 10px 20px;
        margin-top:20px;
        color: white;
        border-radius: 20px;
    }
    .submit{
        text-align:center;
    }

</style>