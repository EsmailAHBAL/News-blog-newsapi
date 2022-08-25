<template>
 <section class="container mt-5">
   <div class="columns is-multiline m-2">
   <div class="column is-4"
   v-for="art in articles" :key="art.source.id">
   <div class="card">
  <header class="card-header">
    <p class="card-header-title">
    <span class="tag is-info">{{art.publishedAt}}</span>
    </p>
    <button class="card-header-icon" aria-label="more options">
      <span class="icon">
        <i class="fas fa-angle-down" aria-hidden="true"></i>
      </span>
    </button>
  </header>
  <div class="card-content">
    <div class="content" style="height: 50vh;">
      <div style="height: 10vh;">

        <span class="tag is-succes mr-2">title</span>{{art.title}}
      </div>
      <hr />
     <div>
      <span class="tag is-dark mr-2">content</span>{{art.content.slice(0,200)}}
      </div>
     <progress class="progress is-small" value="100" max="100"></progress>
     <div class="d-flex justify-content-center" >
      <button class="button is-info is-light is-small"
      @click="toPost(art.author)"
      >Read More</button>


     </div>
    </div>
  </div>

</div>
   </div>
   </div>
 </section>
</template>

<script>
var Md = require('markdown-it')();
export default {
  name: 'IndexPage',
  data:()=>({
    articles:[]
  }),
  mounted(){
    this.getData();
  },
  methods:{
    renderMarkDown(art){
      return Md.render(`# ${art}`);
    },
    toPost(id){
      this.$router.push("/post/"+id)
    },
    getData(){
      const api = `https://newsapi.org/v2/everything?domains=wsj.com&apiKey=5f8ce8e05e814e47822d05da4e46adf7`;
       fetch(api)
       .then(res=>{
        if(res.ok){return res.json();}
       })
       .then(data=>{
        if(data){
          this.articles=data.articles;
        }
       })
    }
  }
}
</script>
