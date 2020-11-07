<template>
  <div class="content peoples">
    
    <div class="peoples__item" v-for="people in peoples" :key="people.index">
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
          <strong>Starships:</strong>
          <div v-for="starship in people.starshipsResults" :key="starship">
            <span>{{starship.name}}</span>
          </div>
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
      // starships: [],
    }
  },
  computed: {
    
  },
  methods: {
    async GetPoples() {

      // axios.get(`${baseUrl}/people/`).then(response => (this.peoples = response.data.results));

      const getPeople = await axios.get(`${baseUrl}/people/`);

      const newRender = [];

      for (let people of getPeople.data.results) {

        const starships = [];

        if (people.starships.length) {
          // Todo: кэшировать запросы
          for(const urlstarship of people.starships) {
            const getStarship = await axios.get(urlstarship);
            starships.push(getStarship.data);
          }

          console.log(people.name);
        }
        
        people.starshipsResults = starships;

        newRender.push(people);
      }

      this.peoples = newRender;

      // this.peoples = getPeople.data.results;
      // console.log(GetPeople);

    },
  },
  mounted(){
    this.GetPoples();
    // this.GetStarships();
  }
}
</script>


<style scoped>

</style>
