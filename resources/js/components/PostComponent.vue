<template>
    <div class="card mt-3">
                <div class="card-header">Posted at: {{post.created_at}} - Updated at: {{post.updated_at}}</div>

                <div class="card-body">
                    <input type="text" class="form-control" v-if="editMode" v-model="post.description">
                    <p v-else>{{post.description}}</p>

                </div>
                <div class="card-footer">
                    <button v-if="editMode" class="btn btn-success" v-on:click="onClickUpdate()">Save</button>
                    <button v-else class="btn btn-default" v-on:click="onClickEdit()">Edit</button>
                    <button class="btn btn-danger" v-on:click="onClickDelete()">Delete</button>
                </div>
            </div>
</template>

<script>
    export default {
        props: ['post'],
        data(){
            return {
                editMode:false
            };
        },
        mounted() {
            console.log('Component mounted.')
        },
        methods:{
            onClickDelete(){
                axios.delete(`/posts/${this.post.id}`).then(() => {
                    this.$emit('delete');
                });
                

            },
            onClickEdit(){
                this.editMode = true;
            },
            onClickUpdate(){
                const params = {
                    description: this.post.description
                };
                axios.put(`/posts/${this.post.id}`, params).then((response) => {
                    this.editMode = false;
                    const post = response.data;
                    this.$emit('update', post);
                });
                
            }
        }
    }
</script>
