<template>
    <div>
    <h1>Vue hh project</h1>
    <template v-if="vacanciesFetched">
      <p>Данные загружены</p>
      <vacancies-cities :cities="cities" />
    </template>

    <p v-else>Загружаем свежайшие вакансии...</p>
  </div>
</template>

<script>
import axios from "axios";
import VacanciesCities from "./VacanciesCities";

export default {
  data() {
    return {
      vacancies: [],
      vacanciesFetched: false,
      cities: []
    };
  },
  components: {
    "vacancies-cities": VacanciesCities
  },
  created() {
    axios
      .get("https://api.myjson.com/bins/1077os")
      .then(response => {
        this.vacancies = response.data;
      })
      .catch(function(error) {
        console.log(error);
      });
  },
  watch: {
    vacancies() {
      this.getCities();
      this.vacanciesFetched = true;
    }
  },
  methods: {
    getCities() {
      let set = new Set();
      this.vacancies.forEach(vacanсy => {
        let city = vacanсy.addr.match(/[а-я-]+/i);
        set.add(city[0]);
      });
      this.cities = Array.from(set);
      this.cities.sort((a, b) => (a > b ? 1 : -1));
    }
  }
};
</script>

<style>
</style>
