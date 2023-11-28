<script setup>
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
      movies: [
        { name: "Deadpool", poster: "images/deadpool.jpeg", type: "Spennumynd, Ævintýri, Gamanmynd" },
        { name: "Shawshank Redemption", poster: "images/shawsank.jpg", type: "Drama" },
        { name: "Spider-man: No Way home", poster: "images/nowayhome.jpg", type: "Spennumynd, Ævintýri, Fantasía" },
      ]
      //["Deadpool", "Shawshank Redemption", "Spider-man: No Way home"],
    }
  }
}


</script>


<template class="movieList">


  <strong><h1 class="text-center mb-4">Væntanleg</h1></strong>


  <div class="about">
    <p>{{name}}</p>
    <div class="w-full">
      <div class="mb-6" v-for="movie in movies">
        <div class="bio bg intro flex justify-start bg-white p-3 ml-2 border-2 border-black">
          <img class="poster" :src="movie.poster" alt="Italian Trulli">
          <div class="ml-2 flex-1">
            <div class="flex justify-between items-center">
              <RouterLink class="mr-4 hover:text-blue-500 text-xl" to="/about">
                <strong>{{ movie.name }}</strong>
              </RouterLink>

            </div>
            <div class="mb-10">
              {{ movie.type}}
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
</style>