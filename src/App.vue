<script setup>
import {ref,computed} from 'vue'
import TheCarousel from './components/TheCarousel.vue'
import { frog, gg, gg_home, gg_event, gg_table, 
gr_home, gr_collection, gr_recipe, gr_signup, test_gif, pool, portrait, NineBall } from './assets';



const selectedCarouselId = ref('Good Game')

const nameIndex = ref(0);

const retInd = (project) => {
  
  selectedCarouselId.value = project;

  nameIndex.value = projects.value.findIndex(project => project.name === selectedCarouselId.value);
  
}

const goRepo = (x) => {
  const project = projects.value[x];
  window.open(project.repoLink, '_blank');
};

const goDemo = (x) => {
  const project = projects.value[x];
  window.open(project.demoLink, '_blank');
};
const projects = ref([
  {
    name: 'Good Game',
    logo: gg,
    repoLink: 'https://github.com/StanPham/Good-Game-App',
    demoLink: 'https://good-game-dev-environment.web.app/',
    home: gg_home,
    s_desc: `Full stack collaboration webdev project for a local business using Vue+Firebase.`,
    items: [
      { title: "Home Page", pic: gg_home},
      { title: "Events", pic: gg_event},
      { title: "Reserve Tables", pic: gg_table},
      { title: "Admin Event Tab", pic: test_gif},
      
    ],
    info: [
      {
        heading: 'Overview',
        content: `A final semester project where groups of four found local clients and built them a full stack application.
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
    home: gr_home,
    s_desc: `Solo project for a recipe website using Vue+Firebase.`,
    items: [
      { title: "Home Page", pic: gr_home},
      { title: "User Collections", pic: gr_collection},
      { title: "Recipe", pic: gr_recipe},
      { title: "Signup", pic: gr_signup},
    ],
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
  {
    name: 'Animejs Collection',
    logo: NineBall,
    repoLink: 'https://github.com/WinnerxSinclair/animejs',
    demoLink: 'https://winnerxsinclair.github.io/animejs/',
    home: pool,
    s_desc: `Collection of basic Animejs projects. Mobile unfriendly.`,
    items: [
      { title: "9-ball", pic: pool},
      { title: "Day2Night", pic: portrait},
      
    ],
    info: [
      {
        heading: 'Overview',
        content: `Small solo animation projects for the purpose of learning css animation and Anime.js`
      },
      {
        heading: 'Technologies Used',
        content: 'Vue, JavaScript, CSS, HTML, Nodejs, Animejs'
      },
      
    ]
  },
])

const carOrAbout = ref(true);
</script>

<template>
  <div class="custom-grid">
    <div class="header light">
      <div class="intro flex gap">
        <img src="./assets/WS.webp" alt="" class="pp">
        <div>
          <h1 class="ff-2">Project Portfolio</h1>
          <p class="ff-1">by Jonathan Malise</p>
        </div>
      </div>
      
      <section class="contact flex column gap">
        <h3 class="underline ff-2">Contact</h3>
        <div class="flex gap">
          <img class="icon-small" src="./assets/email-outline.png" alt="">
          <p class="ff-1">jmalise2000@gmail.com</p>
        </div>
        <div class="flex gap">
          <img class="icon-small" src="./assets/phone.png" alt="">
          <p class="ff-1">(479) 970-1547</p>
        </div>
      </section>
    </div>
    
    <nav class="sidebar flex align-c column">
      <h1 class="underline margin-top">Project List</h1>
      <ul class="bold">
        <li class="click" :class="{blackBlur: selectedCarouselId == project.name}"
        @click="retInd(project.name)"
        v-for="(project,index) in projects" :key="index" :value="project.name">
          <img :src="project.logo" alt="" class="icon-small">
          <div class="fs-200" >{{project.name}}</div>
        </li>
      </ul>
    </nav>
    <main class="content">
      <div class="app-title flex-c-c">
        <div class="flex-c-c gap title-wrap">
          <img class="icon-custom" :src="projects[nameIndex].logo" alt="">
          <h1 class="ff-4 pad">{{ selectedCarouselId }}</h1>
          <img @click="goRepo(nameIndex)" src="./assets/gh_logo.png" alt="" class="icon-small click scale">
          <img @click="goDemo(nameIndex)" src="./assets/link.png" alt="" class="icon-small click scale">
        </div>
        <div class="swap-btns">
          <button @click="carOrAbout=true" class="left-btn" :class="{btnBg: carOrAbout}">Carousel</button>
          <button @click="carOrAbout = false" :class="{btnBg: !carOrAbout}" class="right-btn">About</button>
        </div>
      </div>

      <div class="xd">
       
        <template v-for="(project,index) in projects" :key="index">
          <TheCarousel  v-if="carOrAbout && selectedCarouselId == project.name" :items="project.items"  />
        </template>
        <section class="info pad rc light" v-if="!carOrAbout">
          <h2 class="text-center">Project Info</h2>
          <div class="" v-for="chunk in projects[nameIndex].info" :key="chunk">
            <h3 class="underline">{{ chunk.heading }}</h3>
            <p class="fs-100">{{ chunk.content }}</p>
            <br>
          </div>
        </section>
      </div>
    </main>

    <main class="mobile-content">
      <h2>My Projects</h2>
      <div class="card-container">
        <div v-for="(project,index) in projects" class="card">
          <img :src="project.home" alt="">
          <section class="pad">
            <div class="flex gap align-c">
              <img :src="project.logo" alt="" class="icon-small">
              <h4>{{ project.name }}</h4>
              <img @click="goRepo(index)" src="./assets/gh_logo.png" alt="" class="mla icon-small click">
              <img @click="goDemo(index)" src="./assets/link.png" alt="" class="icon-small click">
            </div>
            <p>{{ project.s_desc }}</p>
          </section>
        </div>
      </div>
    </main>
    <section class="m-contact flex column gap light">
        <h3 class="underline">Contact</h3>
        <p class="ff-1">Please give me an email or call if you think our work can be mutually beneficial.</p>
        <div class="flex gap">
          <img class="icon-small" src="./assets/email-outline.png" alt="">
          <p class="ff-1">jmalise2000@gmail.com</p>
        </div>
        <div class="flex gap">
          <img class="icon-small" src="./assets/phone.png" alt="">
          <p class="ff-1">(479) 970-1547</p>
        </div>
      </section>
  </div>
</template>

<style scoped>
@import './mobile.css';
.sidebar li{
  padding:1rem;
}
.btnBg{
  background:purple;
  color:white;
}
.swap-btns{
  margin-left:2rem;
}
.swap-btns button{
  padding: .1em .5em;
}
.left-btn{
  border-radius: 1rem 0 0 1rem;
}
.right-btn{
  border-radius: 0 1rem 1rem 0;
}
.icon-scale{
  width:calc(30px+1vmin);
  height:calc(30px+1vmin);
}
.mla{
  margin-left:auto;
}
.info{
  max-width: 650px;
 
  
}
.dark{
  color:white;
  background:#150026;
}
.light{
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
  display:flex;
}
.contact{
  margin-left:auto;
  align-self:center;
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
  box-shadow: 0 0 2px 1px rgba(60, 64, 67, .3),0 0 6px 2px rgba(60, 64, 67, .15);
  border-radius: 1rem;
}
.content{
  grid-row: 2/3;
  grid-column:2/3;
  background: rgba(255, 255, 238, 0.134);
  padding-left:1px;
}
.xd{
  height:calc(100% - 76.8px);
  max-height: 650px;
  display:grid;
  place-items:center;
  
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
.m-contact{
  display:none;
  padding:3%;
}

@media(max-width: 1050px){
  .sidebar{
    display:none;
  }
  .custom-grid{
    display:block;
  }
  .content{
    display:none;
  }
  .mobile-content{
    display:block;
  }
  .header > section{
    display:none;
  }
  .intro{
    margin-left:auto;
    margin-right:auto;
  }
  .m-contact{
    display:flex;
  }
}

</style>
