<script>
    export default{

        data(){
            return{
                messageButton: 'Récupérer les commentaire',
                text: Object,
                stateComment: false,
            }
        },

        props : {
           postId: Object,
           titleComment: Function 
        },

        methods:{
            async fetchCommentPost(){
                const url = `https://jsonplaceholder.typicode.com/posts/${this.postId.id}/comments`
                this.text = await( await fetch(url)).json()
            },

            toggleComment(){
               this.stateComment = !this.stateComment
            },
        }
    }
</script>

<template>
    <button @click="fetchCommentPost"> {{messageButton}} </button>
    <div>
        <button v-if=" Object.keys(text).length !== 0" @click="toggleComment" class="btn_show_comment"> {{this.stateComment === false ? 'masquer' : 'voir'}} les commentaires</button>
        <ul>
            <li class="box_comment" :class="{state_comment : this.stateComment} " v-for="{body, name} in text">
                <h5 class="title_comment"> {{this.titleComment(name)}} :</h5>
                <p > {{body}} </p>
            </li>
        </ul>
    </div>
    
</template>

<style>
    button{
        margin: 5px;
    }
    .box_comment{
        background-color: rgb(10, 16, 72);
        padding: 5px;
        border-radius: 5px;
        margin: 2px 0 2px 0;
    }

    .title_comment{
        text-align: left;
        padding-left: 5px;
    }
    .state_comment{
        display: none;
    }
    .btn_show_comment{
        background-color: rgb(139, 111, 9);
    }
   
</style>