<template>
    <div class="w-10/12 m-auto">

        <Nav />

        <div v-if="project">

            <div class="flex gap-10">
                <img :src="project.img.url" alt="Projet" class="w-1/3">

                <div>
                    <h1 class="h1-title">{{ project.name }}</h1>
                    <p>{{ project.description }}</p>
                </div>
            </div>

            <hr class="line w-5/6 m-auto">


            <a class="underline" v-if="project.git_link" :href="project.git_link">Lien du github</a>
            <br>
            <a class="underline" v-if="project.web_link" :href="project.web_link">Lien du site </a>


            <div class="flex gap-2 ">
                <p>Langages utilisés :</p>
                <div :key="techno" v-for="techno in project.technos">
                    <img :src="techno.img.url" alt="Technologies" class="w-10">
                </div>
            </div>

            <div class=" flex gap-4">
                <p>Type de projet : {{ project.type }}</p>
            </div>


            <!-- {{ project.id }}
            <a href="">Projet précédent</a>
            <a href="">Projet suivant</a> -->



        </div>
        <!-- <div v-if="projects">
            <nuxt-link to=""></nuxt-link>
            vgyvt
            <nuxt-link to="/" :key="project_list.id" v-for="project_list in projects.data">
                dvsd
                {{ project_list.name }}
            </nuxt-link>
        </div> -->

        <!-- <div v-if="project.value.id">
            {{ projectPrevious.name }}
        </div> -->
    </div>
</template>

<script setup>
definePageMeta({
    layout: "pages",
});

const { find } = useStrapi()
const { findOne } = useStrapi()
const route = useRoute()
const project = ref()

// const projectPrevious = ref()

const projects = ref()


onMounted(async () => {
    project.value = await findOne(`projects?filters[slug]=${route.params.slug}&populate=deep`)
    project.value = project.value.data[0]

    // const previousId = project.value.id - 1
    // projectPrevious.value = await findOne(`projects?filters[id]=${previousId}&populate=deep`)
    // projectPrevious.value = projectPrevious.value.data[0]

    projects.value = await find('projects', { populate: 'deep' })
    console.log(projects.value)
})



</script>

