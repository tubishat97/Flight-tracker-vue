<template>
    <div>
        <nav class="navbar navbar-expand-lg fixed-top navbar-dark bg-dark" aria-label="Main navigation">
            <div class="container-fluid">
                <a class="navbar-brand" href="#">Flight tracker</a>
                <button class="navbar-toggler p-0 border-0" type="button" data-bs-toggle="offcanvas"
                    aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
            </div>
        </nav>
        <main class="container">
            <div class="d-flex align-items-center p-3 my-3 text-white bg-dark rounded shadow-sm">
                <img class="me-3" src="../assets/logo.jpg" alt="" width="48" height="38">
            </div>
            <div class="my-3 p-3 bg-white rounded shadow-sm">
                <b-input-group class="mt-3 mb-3">
                    <b-input-group-prepend is-text>
                        <b-icon icon="search"></b-icon>
                    </b-input-group-prepend>
                    <b-form-input
                        @keyup="search"
                        v-model="flight_number"
                        placeholder="Enter flight number to search..."
                    />
                </b-input-group>
                <b-table striped hover small :items="results" :fields="fields" v-if="results.length > 0"></b-table>
                <div v-else> no rows found</div>
            </div>
        </main>
    </div>
</template>

<script>
export default {
    name: 'Home',
    data() {
        return {
            is_loading: false,
            flight_number: '',
            fields: [
                {
                    key: 'flight_number',
                    label: 'Flight number',
                    
                },
                {
                    key: 'flight_airline.airline_name',
                    label: 'Airline',
                    
                },
                {
                    key: 'flight_from_airport.airport_name',
                    label: 'From Airport',
                    
                },
                {
                    key: 'flight_from_airport.airport_city_location',
                    label: 'From Airport Location',
                    
                },
                {
                    key: 'flight_to_airport.airport_name',
                    label: 'To Airport',
                    
                },
                {
                    key: 'flight_to_airport.airport_city_location',
                    label: 'To Airport Location',
                    
                },
                {
                    key: 'flight_airplane.airplane_name',
                    label: 'Airplane name',
                    
                },
                {
                    key: 'flight_airplane.airplane_max_seat',
                    label: 'Airplane max seat',
                    
                },
                {
                    key: 'flight_airplane.airplane_type',
                    label: 'Airplane type',
                    
                },
            ],
            results: [],
        }
    },
    methods: {
        async search() {
            var results = await this.axios.get(`http://64.227.118.65/api/customer/search?flight_number=${this.flight_number}`);
            this.results = results.data.data
        }
    },
}
</script>

<style scoped>
.bd-placeholder-img {
    font-size: 1.125rem;
    text-anchor: middle;
    -webkit-user-select: none;
    -moz-user-select: none;
    user-select: none;
}

@media (min-width: 768px) {
    .bd-placeholder-img-lg {
        font-size: 3.5rem;
    }
}
</style>
