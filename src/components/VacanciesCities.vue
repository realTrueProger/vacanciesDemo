<template>
    <div>
        <div class="form-group col-3">
            <label for="inputVacansiesCity">Города</label>
            <select id="inputVacansiesCity" class="form-control">
            <option selected>Выберите город...</option>
            <option v-for="(city, index) in cities" :key="index"> {{ city }}</option>
      </select>
    </div>
    </div>
    
</template>

<script>
export default {
    props: ['cities'],
};
</script>

<style>
</style>

