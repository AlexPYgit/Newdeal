<script >
  import Title from './components/Title.vue'
  import Comment from './components/GetCommentPost.vue'

  const API_URL = `https://jsonplaceholder.typicode.com/`
  const Path_Post_URL = 'posts?_limit='

export default {
  components: {
    Title,
    Comment,
  },

  data: () => ({
    getPosts : Object,
    nbrPost:0,
  }),
  
  methods: {
    async fetchData() {
       const url = `${API_URL}${Path_Post_URL}${this.nbrPost}`
       this.getPosts = await (await fetch(url)).json()     
    },
    
    singular(){
      return this.nbrPost > 1 ? ` les ${this.nbrPost} articles` : "l'article"
    },

    titleUppercase(arg){
      return arg.toUpperCase()
    },
    
  }
}
</script>

<template>
  <Title/> 
  <span> Combien d'article souhaitez-vous consulter ?  </span>
	<input class="hallo" v-model="this.nbrPost"> <button @click="fetchData">Récupérer {{singular()}} que vous souhaitez voir.</button>
  <ul v-if="!nbrPost == 0 && nbrPost<=100"> 
    <li class="pointed" v-for=" {id , body, title} in getPosts">
      <span class="message number "> article - {{ id }}</span>
      <h3> {{titleUppercase(title)}} </h3>
      <p class="message">{{body}} </p>
      <Comment 
        :postId="{id}"
        :titleComment="titleUppercase" > 
      </Comment> 
      <br>
    </li>
  </ul>
  <p v-else> veuillez saisir un chiffre entre 1 et 100. </p>
</template>

<style>
  h3{
    margin-top: 0px;
  }
  a {
    text-decoration: none;
    color: #42b883;
  }
  li {
    list-style: none;
    line-height: 1.5em;
    margin-bottom: 20px;
    padding: 5px;
  }
  .number{
    font-size:10px; 
    }
  .author,
  .date {
    font-weight: bold;
  }
  .pointed:hover{
    background-color: rgb(75, 69, 69);
    border-radius: 10px;
  }
  .title:hover {
    filter: drop-shadow(0 0 0.3em #7b81f0aa);
  }
  .hallo:hover {
    filter: drop-shadow(0 0 0.2em #42b883aa);
  }
</style>