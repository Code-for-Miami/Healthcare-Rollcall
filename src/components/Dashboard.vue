<template>
    <b-container fluid="md" id="secure">
        <h1>Dashboard</h1>
        <b-row>
            <b-col>
                <!-- Dashboard Table -->
                <table class="table">
                    <tr>
                        <td>Name</td>
                        <td>Status</td>
                        <td>Updated</td>
                    </tr>
                    <tr v-for="entity in entities" v-bind:key="entity.id">
                        <td><router-link :to="{ name: 'facility', params: { entityID: entity.id }}">{{ entity.name }}</router-link></td>
                        <td>{{ entity.checkIn }}</td>
                        <td>{{ entity.updatedAt }}</td>
                    </tr>
                </table>
            </b-col>
        </b-row>
    </b-container>
</template>

<script>
    import axios from 'axios'

    export default {
        name: 'dashboard',
        data() {
            return {
                api: this.$root.$data.apiEndpoint,
                entities: null
            }
        },
        methods: {
            updateEntities(obj) {
                this.entities = obj;
            }
        },
        created() {
            let self = this;
            axios
                .get(self.api + '/entity')
                .then(function(response) {
                    // Save API response to component data
                    self.updateEntities(response.data.results);
                })
                .catch(function(err) {
                    console.log(err);
                });
        }
    }
</script>

<style scoped>
    h1 {
        text-align: left;
    }

</style>