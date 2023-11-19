<!-- <template>
    <h1>index.vue</h1>
    <LandingBanner v-if="body" :body="dataBanner" />
</template> -->
<template>
    <div v-if="posts">
        <ol>
    <div v-for="post in posts" :key="post.id">
        <li>
            <NuxtLink :to="`/post/${post.id}`" ><h2 v-html="post.title.rendered"></h2></NuxtLink >
            <p v-html="post.excerpt.rendered"></p>
        </li>
    </div>
</ol>

    </div>
    <!-- <div v-for="block in body" :key="block._uid" >
        <LandingBanner v-if="block.component === 'Banner'" :body="block" />
        <Feature v-if="block.component === 'feature'" :body="block"/>
    </div> -->
</template>

<script>
  export default {
      data: function(){
          return{
              body:null,
              posts: null
          }
      },
      created: function() {
          fetch('https://wptavern.com/wp-json/wp/v2/posts?_fields=author,id,excerpt,title,link')
          .then(resp => resp.json())
          .then(data => this.posts = data)
      },
      computed: {
            dataBanner: function(){
                return this.body.find(data => data.component === "Banner")
            }
        }
  }
</script>