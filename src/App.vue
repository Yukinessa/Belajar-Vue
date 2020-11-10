<template>
  <div id="app">
    <Coba />
    <input type="text" v-model="activity" />
    <button @click="addNewTodo">submit</button>
    <ul v-for="(todo,id) in todos" :key="id">
      <li @click="deleteTodo(id)">{{todo}}</li>
    </ul>
    <ul v-for="(anime,id) in animes" :key="id">
      <li>
        <CardAnime :anime="anime" />
      </li>
    </ul>
  </div>
</template>

<script>
import Coba from "./components/Coba";
import CardAnime from "./components/CardAnime";

export default {
  name: "App",
  components: {
    Coba,
    CardAnime
  },
  data: () => ({
    todos: [],
    activity: "",
    animes: []
  }),
  methods: {
    addNewTodo: function() {
      if (this.activity !== "") {
        this.todos = [...this.todos, this.activity];
        this.activity = "";
      }
    },
    deleteTodo: function(id) {
      this.todos = this.todos.filter((todo, idx) => id != idx);
    },
    getTopAnime: function() {
      fetch("https://api.jikan.moe/v3/top/anime")
        .then(response => response.json())
        .then(response => {
          this.animes = response.top;
        });
    }
  },
  mounted() {
    this.getTopAnime();
  }
};
</script>
