<template>
    <div>
        <h1>Vue hh project</h1>

        <template v-if="vacanciesFetched">
            <p>Данные загружены</p>
            <VacanciesCities :cities="cities" />
        </template>

        <p v-else>Загружаем свежайшие вакансии...</p>
        
        <template v-if="error">
            <p>Что то пошло не так, но мы уже работаем над этим. <br /> Вы можете ознакомится с актуальными вакансиями на сайте HeadHunter</p>
            <a href="https://hh.ru/employer/656481">Вакансии Биглион</a>
        </template>
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
      cities: [],
      error: false
    };
  },
  components: {
    VacanciesCities
  },
  created() {
    axios
      .get("https://api.myjson.com/bins/1077os")
      .then(response => {
        this.vacancies = response.data;
        this.getCities();
        this.vacanciesFetched = true;
      })
      .catch(function(error) {
        console.log(error);
        this.error = true;
      });
  },
  methods: {
    getCities() {
      let set = new Set();
      this.vacancies.forEach(({ addr }) => {
        let city = addr.split(",")[0];
        set.add(city);
      });
      this.cities = [...set].sort((a, b) => (a > b ? 1 : -1));
    }
  }
};
</script>

<style>
</style>
