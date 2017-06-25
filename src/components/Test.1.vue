<template>
    <div class="test">
        <input type="test" v-model="title"><br />
        <h1>{{title}}</h1>
        <p v-if="showname">{{user.firstname}}</p>
        <p v-else="showname">Nobody</p>
        <ul>
            <li v-for="item in items">{{item.title}}</li>
        </ul>
        <button v-on:click="greet(title)">Say Greeting</button>
        <input type="text" v-on:keyup="presskey" v-on:keyup.enter="enterhit">
        
        <hr >
        <label>First Name: </label><input type="text" v-model="user.firstname">
        
        <br >
        <label>Last Name: </label><input type="text" v-model="user.lastname">
        
        <h3>{{fullname}}</h3>
    </div>
</template>

<script>
    export default {
        name:'test',
        data() {
            return {
                title: 'Hello World',
                user: {
                    firstname: 'Joe',
                    lastname: 'Bill'
                },
                showname: true,
                items: [
                    {title:'Item One'},
                    {title:'Item Two'},
                    {title:'Item Three'}
                    ]
                
            }
        },
        methods: {
            greet: function(greeting){
                alert(greeting);
            },
            presskey: function(e){
                console.log(e.target.value);
            },
            enterhit: function() {
                console.log('You hit enter');
            }
        },
        computed: {
            fullname: function(){
                return this.user.firstname + " " + this.user.lastname;
            }
        }
    }
</script>

<style scoped>
    
</style>