<template>
    <div class="card">
                <div class="card-header">what are you thinking?</div>

                <div class="card-body">
                                      
                    <form action="" v-on:submit.prevent="newPost()" >
                        <div class="form-group">
                            <label for="post">Post a message</label>
                            <input class="form-control" type="text" name="post" v-model="description">
                        </div>
                        <button type="submit" class="btn btn-primary">Post</button>
                    </form>
                </div>
            </div>
</template>

<script>
    export default {
        data(){
            return {
                description: ''
            }
        },
        mounted() {
            console.log('Component mounted.')
        },
        methods: {
            newPost(){
                const params = {
                    description: this.description
                };
                this.description = '';
                axios.post('/posts', params).then((response) => {
                    const post = response.data;
                    this.$emit('new', post);
                });
                
                
                
            }
        }
    }
</script>
