<template>
  <section class="container mt-5">
    <div class="card">
       <div class="card-content">
        <div class="content">
          <div>
            <span class="tag is-danger mr-3">Title</span> {{atricle.title}}
          </div>

          <hr />
         <span class="tag is-danger mr-3">Content</span> {{atricle.content}}
          <div class="mt-5">
             <img :src="atricle.urlToImage" class="w-50"/>
          </div>
             <div class="mt-5">
            <span class="tag is-primary mr-3">Description</span> <p v-html="atricle.description"></p>
          </div>

         <div class="mt-3 d-flex justify-content-around">
          <span class="tag is-primary">{{atricle.author}}</span>
          <span class="tag is-info">{{atricle.publishedAt}}</span>
          <span class="tag is-succes">{{atricle.url}}</span>

         </div>
       </div>
  </div>
</div>
  </section>
</template>
<script>
export default {
  data:()=>({
   all:[],
   atricle : {}
  }),
  mounted(){
    this.getPost()

  },
  methods:{
    async getPost(){
     const api=`https://newsapi.org/v2/everything?domains=wsj.com&apiKey=5f8ce8e05e814e47822d05da4e46adf7`;
     fetch(api)
     .then(res=>{
      if(res.ok)
      {return res.json()}
      })

     .then(data=>{
      if(data){
      this.all=data.articles;
       this.all.filter(
        item => {
          if(item.author == this.$route.params.id){
            this.atricle = item;
          }
        }
       )
       }

     })
    },



  }
}
</script>
