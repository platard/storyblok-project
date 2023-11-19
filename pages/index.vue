<template>
    <div v-if="body" v-for="block in body" :key="block._uid" >
        <Banner v-if="block.component === 'Banner'" :block="block" />
    </div>
    <!-- <Teaser v-if="block.component === 'teaser'" :blok="block" /> -->
</template>
<!-- <template >
    <h1>index.vue</h1>
    <div v-if="body">
        <Banner  :body="dataBanner" />
    </div>
    <Feature :body="body" />
    <div v-if="body">
        <h2>{{ body[0].Title }}</h2>
        <p>{{ body[0].subtitle }}</p>
    </div>
    <div v-if="body">
        <h2>{{ body[1].name }}</h2>
        <img :src="body[1].image.filename" alt="">
    </div>
</template> -->

<script>
  export default {
      data: function(){
          return{
              body:null
          }
      },
    
    async created() {
        try {
        const response = await fetch('https://api-us.storyblok.com/v2/cdn/stories/home?version=draft&token=HEYrNygm9QDpTLSPmXmNAgtt&cv=1700417322')
        const data = await response.json(); // Set the body data property to the fetched JSON
        this.body = data.story.content.body
        } catch (error) {
        console.error('Error fetching data:', error); // Handle any errors
        }
    },
    computed: {
        dataBanner: function(){
            return this.body.find(data => data.component === "Banner")
        }
    }
  }
</script>