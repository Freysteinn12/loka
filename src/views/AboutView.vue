<script setup>
import axios from 'axios';
import TheWelcome from '../components/TheWelcome.vue'
import { Dropdown, ListGroup, ListGroupItem } from 'flowbite-vue'
import {RouterLink} from "vue-router";
</script>

<script>
import {RouterLink} from "vue-router";
import {Dropdown, ListGroup, ListGroupItem} from "flowbite-vue";

export default {
  components: {Dropdown, RouterLink, ListGroup, ListGroupItem},
  data() {
    return {
      movies: []
    }
  },
  mounted() {
    axios.get('https://grouplimit.co/api/v1/cinema/LFZHAia7t0NjjJ62F2pB')
        .then((response) => {
          // handle success
          this.movies = response.data.data
        })
        .catch(function (error) {
          // handle error
          console.log(error);
        })
        .finally(function () {
          // always executed
        });
  }
}


</script>




<template class="movieList">

  <strong><h1 class="text-center mb-4">Vinsælar</h1></strong>

  <div class="dropdowns mb-10">
    <dropdown class="ml-2"  placement="bottom" text="Staður">
      <list-group>
        <list-group-item class="p-3">
          <RouterLink to="/home">Allir</RouterLink>
        </list-group-item>
        <list-group-item class="p-3">
          <RouterLink to="/home?location=Sambíóin Kringlunni">Sambíóin Kringlunni</RouterLink>
        </list-group-item>
        <list-group-item class="p-3">
          <RouterLink to="/home?location=Sambíóin Álfabakka">Sambíóin Álfabakka</RouterLink>
        </list-group-item>
        <list-group-item class="p-3">
          <RouterLink to="/home?location=Sambíóin Egilshöll">Sambíóin Egilshöll</RouterLink>
        </list-group-item>
        <list-group-item class="p-3">
          <RouterLink to="/home?location=Sambíóin Akureyri">Sambíóin Akureyri</RouterLink>
        </list-group-item>
        <list-group-item class="p-3">
          <RouterLink to="/home?location=Sambíó">Sambíó</RouterLink>
        </list-group-item>
        <list-group-item class="p-3">
          <RouterLink to="/home?location=Laugarásbíó">Laugarásbíó</RouterLink>
        </list-group-item>
      </list-group>
    </dropdown>


    <dropdown class="ml-2" placement="bottom" text="Frumsýnd klukkan">
      <list-group>
        <list-group-item class="p-3">
          <RouterLink to="/home">Allar</RouterLink>
        </list-group-item>
        <list-group-item class="p-3">
          <RouterLink to="/home?from=13">Frá 13:00</RouterLink>
        </list-group-item>
        <list-group-item class="p-3">
          <RouterLink to="/home?from=14">Frá 14:00</RouterLink>
        </list-group-item>
        <list-group-item class="p-3">
          <RouterLink to="/home?from=15">Frá 15:00</RouterLink>
        </list-group-item>
        <list-group-item class="p-3">
          <RouterLink to="/home?from=16">Frá 16:00</RouterLink>
        </list-group-item>
        <list-group-item class="p-3">
          <RouterLink to="/home?from=17">Frá 17:00</RouterLink>
        </list-group-item>
        <list-group-item class="p-3">
          <RouterLink to="/home?from=18">Frá 18:00</RouterLink>
        </list-group-item>
        <list-group-item class="p-3">
          <RouterLink to="/home?from=19">Frá 19:00</RouterLink>
        </list-group-item>
        <list-group-item class="p-3">
          <RouterLink to="/home?from=20">Frá 20:00</RouterLink>
        </list-group-item>
        <list-group-item class="p-3">
          <RouterLink to="/home?from=21">Frá 21:00</RouterLink>
        </list-group-item>
        <list-group-item class="p-3">
          <RouterLink to="/home?from=22">Frá 22:00</RouterLink>
        </list-group-item>
      </list-group>
    </dropdown>



  </div>

  <div class="about">
    <p>{{name}}</p>
    <div class="row w-full flex flex-wrap">
      <div class="page mb-6 w-1/3" v-for="movie in movies">
        <div class="bio bg intro flex justify-start bg-white p-3 ml-2 border-2 border-black">
          <img class="poster" :src="movie.poster" alt="Italian Trulli">
          <div class="ml-2 flex-1">
            <div class="flex justify-between items-center">
              <strong class="mr-4 hover:text-blue-500 text-xl">{{ movie.name }} ({{ movie.year }})</strong>

              <p class="rating"> {{ movie.imdb_rating }} </p>
            </div>
            <div class="mb-10">
              <strong>{{ movie.age_restriction }}</strong>
            </div>


            <div class="mb-6" v-for="(showtime, name) in movie.showtimes">
              <p v-if=" ! $route.query.location">{{ name }}</p>
              <strong><p v-if="name == $route.query.location">{{ name }}</p></strong>

              <div v-if=" movie.imdb_rating >= 7">
                <strong>{{ show.time }} - {{ show.location }}</strong>
              </div>

              <div v-for=" show in showtime" v-if="$route.query.location == null">
                <div v-if=" ! $route.query.from">
                  {{ show.time }} - {{ show.location }}
                </div>

                <div v-if="show.time.substring(0,2) >= $route.query.from">
                  <strong>{{ show.time }} - {{ show.location }}</strong>
                </div>
              </div>

              <div v-for=" show in showtime" v-else-if="name == $route.query.location">
                <div v-if=" ! $route.query.from">
                  {{ show.time }} - {{ show.location }}
                </div>

                <div v-if="show.time.substring(0,2) >= $route.query.from">
                  <strong>{{ show.time }} - {{ show.location }}</strong>
                </div>

              </div>
            </div>

          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<style>
* {
  box-sizing: border-box;
}

html, body {
  height: 100%;
}

body {
  display: grid;
}

h1 {
  font-size: 30px;
}

ul {
  display: flex;
  width: 50%;
}

.bg {
  border-radius: 5px;

}

.bio {
  height: 100%;
}


.about {
  display: flex;
  justify-content: start;
  padding: 20px;
  margin-left: 100px;
  margin-right: 100px;
  background-color: #90a0a6;
  border-radius: 8px;
}

.rating {
  background-color: #2c3e50;
  color: white;
  width: 50px;
  height: 50px;
  border-radius: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.rating:hover {
  background-color: #7e9eb6;
}


.dropdowns {
  display: flex;
  align-items: center;
  justify-content: center;
  border-color: black;
}

.poster {
  width: 200px;
  height: 300px;
}



@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
  }
}
@media (max-width: 1100px) {
  .page {
    width: 100%;
  }
}
</style>