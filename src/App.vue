<script setup>
import { ref, computed, onMounted } from 'vue';
import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';


// const posts = ref([
//   {title: 'Post 1', id: 1, body: 'Dscripcion 1'},
//   {title: 'Post 2', id: 2, body: 'Dscripcion 2'},
//   {title: 'Post 3', id: 3, body: 'Dscripcion 3'},
//   {title: 'Post 4', id: 4},
// ]);


const posts = ref([]);
const favorite = ref('');
const postXpage = 10;
const startPage = ref(0);
const endPage = ref(postXpage);
const loading = ref(true);



const changeFavourite = (title) => {
  favorite.value = title;
} 




const next = () => {
  startPage.value = startPage.value + postXpage;
  endPage.value = endPage.value + postXpage;
}

const prev = () => {
  startPage.value = startPage.value - postXpage;
  endPage.value = endPage.value - postXpage;
}





// 1.- Metodo con onMounted
// onMounted(() => {
//fetchData()
// });


// 2.- Metodo Con Fecth
// fetch('https://jsonplaceholder.typicode.com/posts')
//     .then(res => res.json())
//     .then(data => {
//       posts.value = data
//     })
//     .catch(e => console.log(e))
//     .finally(() => {
//       setTimeout(() => {
//         loading.value = false;
//       }, 2000)
//     });


// 3.- Con metodo
const fetchData = async() => {
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts')
    posts.value = await res.json()
  } catch (error) {
    console.log(error)
  }finally{
      setTimeout(() => {
        loading.value = false;
      }, 2000)
  }
}
fetchData();








const maxLength = computed(() => posts.value.length)

</script>


<template>

  <LoadingSpinner v-if="loading" />
  

  <div class="container" v-else>

    <h1>APP</h1> 

    <h2>Mis Post Favorito: {{favorite}} </h2>


    <PaginatePost 
      @next="next"
      @prev="prev"
      :startPage="startPage"
      :endPage="endPage"
      :maxLength="maxLength"
      class="mb-2"
    />
  


    <BlogPost 
      v-for="post in posts.slice(startPage, endPage)"
      :key="post.id"
      :title="post.title"
      :id="post.id"
      :body="post.body" 
      @changeFavourite="changeFavourite"
      class="mb-2"
    ></BlogPost>

  </div>

</template>