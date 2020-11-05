<template>
  <div class="content peoples">
    
    <div class="peoples__item" v-for="people in peoples" :key="people">
      <div class="peoples__name">
        {{people.name}}
      </div>
      <div class="peoples__characteristics">
        <div class="peoples__characteristics-params">
          <p>Gender: <strong>{{people.gender}}</strong> </p>
          <p>Height: <strong>{{people.height}}</strong> </p>
          <p>Mass: <strong>{{people.mass}}</strong> </p>
        </div>
        <div class="peoples__characteristics-starship">
          <strong>Starships</strong>
        </div>
      </div>
      
    </div>

  </div>
</template>

<script>
import axios from 'axios';
const baseUrl = 'https://swapi.dev/api';
export default {
  name: 'ListPerson',
  data() {
    return {
      peoples: [],
    }
  },
  computed: {
    
  },
  methods: {
    GetPoples() {
      axios.get(`${baseUrl}/people/`).then(response => (this.peoples = response.data.results));
    },
  },
  mounted(){
    this.GetPoples();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
