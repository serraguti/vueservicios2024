<template>
    <div>
        <h1>Customers Component</h1>
        <form v-on:submit.prevent="buscarCustomer()">
            <label>Id Cliente</label>
            <input type="text" v-model="idCustomer"/>
            <button>
                Buscar Customer
            </button>
        </form>
        <div v-if="customer">
            <h2>Nombre: {{ customer.contactName }}</h2>
            <h2>Compañia: {{customer.companyName}}</h2>
            <h2>Título: {{customer.contactTitle}}</h2>
        </div>
        <table border="1">
            <thead>
                <tr>
                    <th>Nombre</th>
                    <th>Empresa</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="customer in customers" :key="customer">
                    <td>{{customer.contactName}}</td>
                    <td> {{ customer.companyName }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
import axios from 'axios';
import Global from './../Global';

    export default {
        name: "CustomersComponent", 
        data() {
            return {
                customers: [],
                idCustomer: "",
                customer: null
            }
        }, 
        mounted() {
            let request = "customers.json";
            let url = Global.urlApiCustomers + request;
            axios.get(url).then(response => {
                console.log("leyendo");
                this.customers = response.data.results;
            })
        },
        methods: {
            buscarCustomer() {
                let request = "customers/" + this.idCustomer + ".json";
                let url = Global.urlApiCustomers + request;
                axios.get(url).then(response => {
                    console.log("Buscando customer");
                    this.customer = response.data.customer;
                })
            }
        }
    }
</script>