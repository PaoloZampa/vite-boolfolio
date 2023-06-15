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
    methods: {
        getProjects(url) {
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
        getImagePath(path) {
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
    <div class="p-5 mb-4 bg-dark">
        <div class="container-fluid py-5">
            <h1 class="display-5 fw-bold text-info">Paolo Zampa</h1>
            <p class="col-md-8 fs-4 text-white">Negli ultimi anni, mi sono dedicato a imparare e padroneggiare la libreria JavaScript
                di React, che considero uno strumento straordinario per la creazione di interfacce utente moderne e
                coinvolgenti. Ho avuto l'opportunità di lavorare su diversi progetti che mi hanno permesso di acquisire una
                vasta esperienza nel creare componenti funzionali, gestire lo stato dell'applicazione e utilizzare librerie
                complementari come Redux o Context API per una gestione avanzata dello stato.</p>
            <button class="btn btn-info btn-lg my-3" type="button">Scoprimi</button>
        </div>
    </div>
    <section class="projects">
        <div class="container">
            <div class="row row-cols-1 row-cols-md-3 row-cols-lg-4">

                <div class="col" v-for="project in projects">
                    <div class="card h-100 rounded-0 shadow">
                        <img class="card-img-top rounded-0" :src="getImagePath(project.image)" alt="">
                        <div class="card-body">
                            <h4>
                                {{ project.name }}
                            </h4>
                        </div>
                        <div class="card-footer">
                            <span class="badge text-bg-info text-white">{{ project.id }}</span>
                        </div>

                    </div>
                </div>

            </div>
        </div>
    </section>
</template>

<style lang="scss">@use './styles/general.scss';</style>
