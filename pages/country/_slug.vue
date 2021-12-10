<template>
<div>
    <v-row align="center"
    justify="space-around">
   <v-btn @click="dataLabel='confirmed'">Confirmed</v-btn>
   <v-btn @click="dataLabel='deaths'">Deaths</v-btn>
   <v-col cols="3">
    <v-menu>
         <template v-slot:activator="{ on, attrs }">
        <v-text-field :value="from" label="From" prepend-icon="mdi-calendar" v-bind="attrs" v-on="on"></v-text-field>
         </template>
        <v-date-picker v-model="from" :min="minDateFrom" :max="to" @click:date="update"></v-date-picker>
    </v-menu>
   </v-col>
   <v-col cols="3">
    <v-menu>
        <template v-slot:activator="{ on, attrs }">
        <v-text-field :value="to" label="To" prepend-icon="mdi-calendar"  v-bind="attrs" v-on="on"></v-text-field>
        </template>
        <v-date-picker v-model="to" :min="from" :max="maxDateTo"></v-date-picker>
    </v-menu>
   </v-col>
   </v-row>
   <chart :data="$store.getters[dataLabel]" :labels="$store.getters.labels" :dataLabel="dataLabel"></chart>
</div>
</template>

<script>

import Chart from '~/components/Chart.vue';
export default {
    components: { Chart },
    created(){
        this.$store.dispatch('getCountry', this.$route.params.slug);
    },
    data(){
        return {
            dataLabel: 'confirmed',
            from: '2020-01-22',
            to: new Date().toISOString().substr(0, 10),
            minDateFrom: '2020-01-22',
            maxDateTo: new Date().toISOString().substr(0, 10),
        }
    }
}
</script>

<style>

</style>