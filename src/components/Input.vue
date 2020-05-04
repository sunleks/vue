<template>
    <div>
        <input type="text" v-model="query">
        <button @click = "onClick">send request</button>
        <br></br>
        <table>
           <caption>Temperature in {{query}}</caption>
                <tr>
                    <th v-for = 'item in this.info'>{{item.dt_txt}}</th>
                </tr>
                <tr>
                    <td v-for = 'item in this.info'>Temp = {{item.main.temp}}</td>
                </tr>
        </table>
    </div>
</template>

<script>
import Vue from 'vue'
import axios from 'axios';

export default {    
    data: { 
        info: '',
        query: ''
    },
    methods: {
        onClick() {
            axios 
            .get(`https://cors-anywhere.herokuapp.com/api.openweathermap.org/data/2.5/forecast?q=${this.query}&appid=ad628c3ff34d34a2909a06ce888926bd`)
            .then((response) => {
                this.info = response.data.list;
                    console.log(this.info);
                let massWeather = [];
                let massTemp = [];

                for (const key in this.info) {
                massWeather.push(this.info[key].dt_txt);
                massTemp.push(this.info[key].main.temp);
                }
                this.renderChart(massWeather, massTemp);
            });          
        }
    }
}
</script>

<style scoped>
    table {
        width: 1000px; 
        border: 1px solid black; 
        border-collapse: collapse;
    }   

    tr {
        width: 100%;
    }

    th {
        border: 1px solid black;
    }
    td {
        border: 1px solid black;
    }
</style>