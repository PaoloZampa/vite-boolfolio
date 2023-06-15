<script>
import axios from "axios";


export default {
    components: {
       
    },
    data() {
        return {
            base_API: 'http://127.0.0.1:8000/',
            project_path: 'api/projects',
            loading: true,
            posts: null
        }
    },
    methods:{
        getProjects(url){
            axios
            .get(url)
            .then(response => {
                console.log(response);
            })
            .catch(error => {
                console.log(error);
            })
        }
    },
    mounted() {
        const url = this.base_API + this.project_path
        this.getProjects(url)
    },

}
</script>

<template>
    <section class="vue-home">
        <div class="container">
            <div class="row">
                
            </div>
        </div>
    </section>
</template>

<style lang="scss">
@use './styles/general.scss';


</style>
