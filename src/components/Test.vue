<template>
    <div>
        <h4>
            Test template
        </h4>
        <input type="text" v-model="searchItem" placeholder="Search">
        <ul v-for="post in filtersearch" :key="post.id">
            <li><b>{{ post.title }}</b></li>
            <li>{{ post.body }}</li>
        </ul>
    </div>
</template>

<script>
    import axios from 'axios';
    export default {
        name: "Test",
        data:function () {
            return{
                posts:[],
                searchItem:''
            }
        },
        created() {
            axios.get('https://jsonplaceholder.typicode.com/posts')
                .then(res =>{
                    this.posts=res.data;
                    //console.log(res);
                })
                .catch(err => {
                    console.log(err);
                })
        },

        computed:{
            filtersearch(){
                return this.posts.filter(post => {
                    return post.title.match(this.searchItem)
                })
            }
        }
    }
</script>

<style scoped>
    ul{
        list-style: none;
    }
</style>