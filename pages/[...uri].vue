<script setup>

const route = useRoute();
const uri = route.params.uri.join('/');
const config = useRuntimeConfig();
const {data, pending, refresh, error} = await useFetch(config.public.wordpressUrl, {
  method: 'get',
  query: {
    query: `
       query MyQuery3($uri: String!) {
           nodeByUri(uri: $uri) {
               ... on Post {
                   id
                   title
                   date
                   content
               }
           }
       }
       `,
    variables: {
      uri: uri
    }
  },
  transform(data){
    return data.data.nodeByUri
  }
})


useHead({
  title: data.value.title
})
</script>



<template>
  <Header></Header>
  <main class="justify-start bg-gray-50 container mx-auto mt-2 p-8">
    <h1 class="text-2xl font-semibold">{{data.title}}</h1>
    <p class="font-thin text-sm">{{ new Date(data.date).toLocaleDateString()}}</p>
    <article class="mt-4 space-y-2" v-html="data.content"></article>
  </main>
</template>