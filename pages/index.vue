<!-- <template>
    <h1>index.vue</h1>
    <LandingBanner v-if="body" :body="dataBanner" />
</template> -->
<template v-if="body">
    <!-- <div v-if="posts">
        <ol>
    <div v-for="post in posts" :key="post.id">
        <li>
            <NuxtLink :to="`/post/${post.id}`" ><h2 v-html="post.title.rendered"></h2></NuxtLink >
            <p v-html="post.excerpt.rendered"></p>
        </li>
    </div>
</ol>

    </div> -->
    <div v-for="block in body" :key="block._uid" >
        <LandingBanner v-if="block.component === 'Banner'" :body="block" />
        <Feature v-if="block.component === 'feature'" :body="block"/>
    </div>
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
          fetch('https://api-us.storyblok.com/v2/cdn/stories/home?version=draft&token=HEYrNygm9QDpTLSPmXmNAgtt&cv=1700417322')
          .then(resp => resp.json())
          .then(data => this.body = data.story.content.body)
      },
      computed: {
            dataBanner: function(){
                return this.body.find(data => data.component === "Banner")
            }
        }
  }
</script>