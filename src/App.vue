<script>
import axios from "axios";


export default {
    components: {
       
    },
    data() {
        return {
            base_url: 'http://127.0.0.1:8000/',
            project_API: 'api/projects',
            loading: true,
            projects: null,
            error: null,
        }
    },
    methods:{
        getProjects(url){
            axios
            .get(url)
            .then(response => {
                console.log(response);
                this.projects = response.data.projects
                this.loading = false
            })
            .catch(error => {
                console.log(error);
                this.error = error.message
            })
        },
        getImagePath(path){
            return this.base_url + 'storage/' + path;
        }
    },
    mounted() {
        const url = this.base_url + this.project_API
        this.getProjects(url)
    },

}
</script>

<template>
    <div class="p-5 mb-4 bg-light rounded-3">
        <div class="container-fluid py-5">
          <h1 class="display-5 fw-bold">Custom jumbotron</h1>
          <p class="col-md-8 fs-4">Using a series of utilities, you can create this jumbotron, just like the one in previous versions of Bootstrap. Check out the examples below for how you can remix and restyle it to your liking.</p>
          <button class="btn btn-primary btn-lg" type="button">Example button</button>
        </div>
      </div>
    <section class="projects">
        <div class="container">
            <div class="row row-cols-1 row-cols-md-3 row-cols-lg-4">

                <div class="col" v-for="project in projects">
                    <div class="card h-100 rounded-0 shadow">
                        <img class="card-img-top" :src="getImagePath(project.image)" alt="">
                        <div class="card-body">
                            <h4>
                                {{ project.name }}
                            </h4>
                        </div>

                    </div>
                </div>
                
            </div>
        </div>
    </section>
</template>

<style lang="scss">
@use './styles/general.scss';


</style>
