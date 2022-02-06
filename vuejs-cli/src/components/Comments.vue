<template>
    <div class="container">
        <h1>Comentários</h1>
        <hr/>
        <div class="form-todo form-group">
            <p>
                <input type="text" placeholder="nome" name="author" class="form-control" v-model="name">
            </p>
            <p>
                <textarea name="message" placeholder="Comentário" class="form-control" v-model="message"></textarea>
            </p>
            <button v-on:click="addComment" type="submit" class="btn btn-primary">Comentar</button>
        </div>
        <div class="list-group">
            <div class="list-group-item" v-bind="(comment, index) in allComments">
                <span class="comment_author">Autor: <strong>{{comment.name}}</strong></span>
                <p>{{comment.message}}</p>
                <div>
                    <a href="#" title="Excluir" v-on:click.prevent="removeComment(index)">Excluir</a>
                </div>
            </div>
        </div>
        <hr/>
    </div>
</template>

<script>
export default {
    data() {
            return {
                comments: [],
                name: '',
                message: ''
            }
        }, 
        methods: {
            addComment() {
                if(this.message.trim() === ''){
                    return;
                }
                this.comments.push({
                    name: this.name,
                    message: this.message
                });

                this.name = '',
                this.message = ''
            },
            removeComment(index) {
                this.comments.splice(index, 1);
            }
        },
        computed: {
            allComments(){
                return this.comments.map(comment => ({
                    ...comment,
                    name: comment.name.trim() === '' ? 'Anônimo' : comment.name
                }))
            }
        },
        watch: {
            comments() {
                
            }
        }
};
</script>

            