<template>
    <div>
        <h1> Fake REST-API Data</h1>
        <div v-if="loading"> Загрузка данных... </div>
        <div v-else> 

            <ul>
                <li v-for="item in data" :key="item.id">{{item.name }} </li>
            </ul>
        </div>
    </div>
    
    </template>


<script> 
import axios from "axios";

export default {
    data(){
        return {
            data: [],
            loading: true, 
        };
    },
    created(){
        this.fetchData();
    },
    methods: {
        fetchData(){
            return new Promise((resolve, reject) =>{
            axios
                .get("https://jsonplaceholder.typicode.com/users")
                .then((response) =>{
                    this.data = response.data
                    this.loading = false;
                    resolve(); // разрешаем промис в случае успеха запроса
                })
                .catch((error) =>{
                    console.error(error);
                    this.loading = false;
                    reject(); //отклоняем промис в случае неудачи
                });
            });
        },
    },
};






</script>