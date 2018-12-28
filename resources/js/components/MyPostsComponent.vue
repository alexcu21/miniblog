<template>
    <div class="row justify-content-center">
        <div class="col-md-8">
            
            <form-component 
                @new="addPost">
                
            </form-component>
            <post-component 
                v-for="(post, index) in posts" 
                :key="post.id"
                :post="post"
                @update="updatePost(post)"
                @delete="deletePost(index)"
                >
                
            </post-component>
        </div>
    </div>
</template>

<script>
    export default {
        data(){
            return {
                posts: []
            }
        },
        mounted() {
            axios.get('/posts').then((response)=>{
                this.posts = response.data;
            });
        },

        methods: {
            addPost(post){
                this.posts.push(post);
            },
             updatePost(index, post){
            this.posts[index] = post; 
           },
           deletePost(index){
            this.posts.splice(index, 1); 
           }
          
        }
    }
</script>
