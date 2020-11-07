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
          <div v-for="starship in people.starshipsResults" :key="starship.index">
            <span v-if="people.starshipsResults == 'false' ">I haven't starship (</span>
            <span v-else>{{starship.name}}</span>
          </div>
        </div>

        <!-- <div v-else class="peoples__characteristics-starship">
          <strong>Starships:</strong>
          <div>
            <span>I haven't starship (</span>
          </div>
        </div> -->

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

      console.time("test");
      for (let people of getPeople.data.results) {

        const starships = [];

        if (people.starships.length) {
          // Todo: кэшировать запросы
          // вариант с последовтаельной загрузкой
          // for(const urlstarship of people.starships) {
          //   const getStarship = await axios.get(urlstarship);
          //   starships.push(getStarship.data);
          // }

          // вариант с параллельной загрузкой 
          const promises = [];
          for (const urlstarship of people.starships) {
            const promise = axios.get(urlstarship);
            promises.push(promise);
          }
          const promisesResult = await Promise.all(promises);
          promisesResult.forEach((starship) => {
            starships.push(starship.data);
          });
          
          // console.log("ответ",promisesResult);

          // console.log(people.name);
        } else {
          // console.log("Нет кораблей", people.name);
          // people.starships.push("нет");
          // people.starships.push(false);
            starships.push(false);
        }
        
        people.starshipsResults = starships;

        newRender.push(people);
      }

      console.timeEnd("test");

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
