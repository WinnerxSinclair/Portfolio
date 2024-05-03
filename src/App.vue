<script setup>
import {ref,computed} from 'vue'
import TheCarousel from './components/TheCarousel.vue'
import { drag, space, frog, gg, gg_home, gg_event, gg_table, gr_home, gr_collection, gr_recipe, gr_signup } from './assets';

const carousels = ref([
  {
    id: 'Good Game',
    items: [
      { title: "Home Page", pic: gg_home},
      { title: "Events", pic: gg_event},
      { title: "Reserve Tables", pic: gg_table},
      
    ]
  },
  {
    id: 'Green Recipes',
    items: [
      { title: "Home Page", pic: gr_home},
      { title: "User Collections", pic: gr_collection},
      { title: "Recipe", pic: gr_recipe},
      { title: "Signup", pic: gr_signup},
    ]
  },
  
])

const selectedCarouselId = ref('Good Game')
const selectedCarouselItems = computed(() => {
  return carousels.value.find(c => c.id === selectedCarouselId.value)?.items || []
})

const nameIndex = ref(0);
const retInd = (project) => {
  selectedCarouselId.value = project;

  for(let i = 0; i<projects.value.length;i++){
    if(projects.value[i].name === selectedCarouselId.value){
      nameIndex.value = i;
    }
  }
}

const goRepo = () => {
  const project = projects.value[nameIndex.value];
  window.open(project.repoLink, '_blank');
};

const goDemo = () => {
  const project = projects.value[nameIndex.value];
  window.open(project.demoLink, '_blank');
};
const projects = ref([
  {
    name: 'Good Game',
    logo: gg,
    repoLink: 'https://github.com/StanPham/Good-Game-App',
    demoLink: 'https://good-game-dev-environment.web.app/',
    info: [
      {
        heading: 'Overview',
        content: `A senior year last semester project where groups of four founds local clients and built them a full stack application.
        The project spanned 4 months and required learning several technologies to complete. Our team made a web application for a local card/board game store called Good Game.
        Main features of the web app are the admin panel, where admins can manipulate docs and collections in the db, and the tabel reservation system, where users
        can reserve tables in advance.`
      },
      {
        heading: 'Technologies Used',
        content: 'Vue, JavaScript, CSS, HTML, Firestore, Nodejs'
      },
      {
        heading: 'My Contribution',
        content: `I was responsible for the entirety of the frontend, as well as portions of backend. It was also my responsibility to find the client
        and schedule meetings with them.`
      }
    ]
  },
  {
    name: 'Green Recipes',
    logo: frog,
    repoLink: 'https://github.com/WinnerxSinclair/Green-Recipes',
    demoLink: 'https://green-recipes-demo.web.app/',
    info: [
      {
        heading: 'Overview',
        content: `A solo project for a recipe website. Users can create collections and then put their own or other people's recipes into those collections.
        Users can also upload recipes to the home page where it is visible to other users -- recipes uploaded here are first checked by admins.`
      },
      {
        heading: 'Technologies Used',
        content: 'Vue, JavaScript, CSS, HTML, Firestore, Nodejs, Algolia'
      },
      {
        heading: 'New Challenges',
        content: `Most new challenges involved backend. Unlike Good Game, this project will have a lot of data if there is many users, so I had to
        implement batch fetching. Also, I needed a reasonable search function which Firestore does not offer, this was solved by linking the db
        to Algolia.`
      }
    ]
  },
])
</script>

<template>
  <div class="custom-grid">
    <div class="header light">
      <div class="intro flex gap">
        <img src="./assets/WS.webp" alt="" class="pp">
        <div>
          <h1>Project Portfolio</h1>
          <p>by Jonathan Malise</p>
        </div>
      </div>
      
      <section class="contact flex column gap">
        <h3 class="underline">Contact</h3>
        <div class="flex gap">
          <img class="icon-small" src="./assets/email-outline.png" alt="">
          <p>jmalise2000@gmail.com</p>
        </div>
        <div class="flex gap">
          <img class="icon-small" src="./assets/phone.png" alt="">
          <p>(479) 970-1547</p>
        </div>
      </section>
    </div>
    
    <nav class="sidebar flex align-c column">
      <h1 class="underline margin-top">Project List</h1>
      <ul class="bold">
        <li class="click" 
        @click="retInd(project.name)"
        v-for="(project,index) in projects" :key="index" :value="project.name">
          <img :src="project.logo" alt="" class="icon-small">
          <div class="whiteBlurHov" :class="{whiteBlur: selectedCarouselId == project.name}">{{project.name}}</div>
        </li>
      </ul>
    </nav>
    <main class="content gg">
      <div class="app-title flex-c-c">
        <div class="flex-c-c gap title-wrap">
          <img class="icon-custom" :src="projects[nameIndex].logo" alt="">
          <h1 class="ff-4 pad">{{ selectedCarouselId }}</h1>
          <img @click="goRepo" src="./assets/gh_logo.png" alt="" class="icon-small click scale">
          <img @click="goDemo" src="./assets/link.png" alt="" class="icon-small click scale">
        </div>
      </div>

      <div class="xd">
        <TheCarousel :items="selectedCarouselItems"/>

        <section class="info">
          <h2 class="text-center">Project Info</h2>
          <div class="pad-left pad-right" v-for="chunk in projects[nameIndex].info" :key="chunk">
            <h3 class="underline">{{ chunk.heading }}</h3>
            <p>{{ chunk.content }}</p>
            <br>
          </div>
        </section>
      </div>
    </main>
  </div>
</template>

<style scoped>
.dark{
  color:white;
  background:#150026;
}
.light{
  color:black;
  background:rgba(255, 253, 195, 0.134);
}

.scale:hover{
  transform:scale(1.1);
}
.icon-custom{
  width:55px;
  aspect-ratio: 1;
}
.custom-grid{
  display:grid;
  grid-template-columns: 1fr 4.5fr;
  grid-template-rows: 20vh 80vh;
  height:100vh;
}
.header{
  grid-column: 1/3;
  grid-row: 1/2;
  display:grid;
  grid-template-columns: 3fr 1fr;
}
.header > *{
  padding:1rem;
}
.intro{
  align-self:center;
}

.sidebar{
  grid-row: 2/3;
  grid-column: 1/2;
  background:rgb(255, 255, 255);
  color:black;
  box-shadow: 1px 0 2px 0 rgba(60, 64, 67, .3),2px 0 6px 2px rgba(60, 64, 67, .15);
  border-radius: 0 1rem 0 0;
}
.content{
  grid-row: 2/3;
  grid-column:2/3;
  color:black;
  background: rgba(255, 255, 238, 0.134);
  padding-left:1px;
}
.xd{
  height:90%;
  display:grid;
  grid-template-columns: 1.5fr 1fr;
  
}
.app-title{
  color:rgb(0, 0, 0);
}
.title-wrap{
  background:rgb(240, 240, 240);
  padding-left:1rem;
  padding-right:1rem;
  border-radius:1rem;
}

.list-header{
  grid-row:1/2;
  grid-column:1/2;
}
ul{
  list-style:none;
}
.sidebar > ul > li{
  margin-top:1rem;
  display:flex;
  align-items:center;
  gap:1rem;
}
.pp{
  width:100px;
  aspect-ratio: 1;
  border-radius:50%;
  object-fit:cover;
}
</style>
