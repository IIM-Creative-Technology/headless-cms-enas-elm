<template>
  <div class="w-10/12 m-auto">

    <Nav />

    <div v-if="projects" class="flex flex-col gap-10 ">
      <h1 class="h1-title">Mes projets</h1>

      <div class="flex justify-between items-center">
        <div class="flex gap-4">
          <p>Filtrer par </p>
          <button @click="chooseFilter = 'technos'" :class="chooseFilter == 'technos' ? 'underline' : ''">
            Technologie
          </button>
          |
          <button @click="chooseFilter = 'types'" :class="chooseFilter == 'types' ? 'underline' : ''">
            Type
          </button>
        </div>


        <div>
          <div v-if="chooseFilter === 'technos'" class="flex gap-8">
            <button class="btn-filter" @click="filterProjectsTechnos('all')">Tout voir</button>
            <button class="btn-filter" :key="techno" v-for="techno in technos" @click="filterProjectsTechnos(techno)">
              {{ techno }}
            </button>
          </div>

          <div v-if="chooseFilter === 'types'" class="flex gap-8">
            <button class="btn-filter" @click="filterProjectsTypes('all')">Tout voir</button>
            <button class="btn-filter" :key="type" v-for="type in types" @click="filterProjectsTypes(type)">{{ type
            }}</button>
          </div>
        </div>
      </div>

      <div class="flex gap-10 ">
        <div class="flex flex-col w-1/2 ">
          <div class="items-center" v-if="chooseFilter === 'technos'" :key="project"
            v-for="project in filteredProjectsTechnos">
            <NuxtLink class="text-xl font-medium" :to="`/projects/${project.slug}`">
              <button @mouseleave="img_src = false" @mouseover="img_src = project.img.url">{{
                project.name }}</button>
            </NuxtLink>
            <hr class="line">
          </div>

          <div class="items-center" v-if="chooseFilter === 'types'" :key="project"
            v-for="project in filteredProjectsTypes">
            <NuxtLink class="text-xl font-medium" :to="`/projects/${project.slug}`">
              <button @mouseleave="img_src = false" @mouseover="img_src = project.img.url">{{
                project.name }}</button>
            </NuxtLink>
            <hr class="line">
          </div>

        </div>



        <div class="w-1/2 grid ">
          <img class="w-2/3 place-self-center" v-if="img_src != false" :src="img_src" alt="Projet" />
        </div>
      </div>

    </div>

  </div>
</template>

<script setup>
definePageMeta({
  layout: "pages",
});


const { find } = useStrapi()

const projects = ref()
const technos = ref([])
const types = ref([])
const activeFilterTechno = ref('all')
const activeFilterType = ref('all')


const chooseFilter = ref('technos')
const img_src = ref(false)


// Filter projects by technology
const filterProjectsTechnos = (techno) => {
  activeFilterTechno.value = techno
}

const filteredProjectsTechnos = computed(() => {
  if (activeFilterTechno.value === 'all') {
    return projects.value.data
  }
  return projects.value.data.filter(project => {
    return project.technos.map(techno => techno.name).includes(activeFilterTechno.value)
  })
})

// Filter projects by type
const filterProjectsTypes = (type) => {
  activeFilterType.value = type
}

const filteredProjectsTypes = computed(() => {
  if (activeFilterType.value === 'all') {
    return projects.value.data
  }
  return projects.value.data.filter(project => project.type === activeFilterType.value)
});


onMounted(async () => {
  // http://localhost:1337/api/projects?populate=*
  projects.value = await find('projects', { populate: 'deep' })
  technos.value = projects.value.data.map(project => {
    return project.technos.map(techno => techno.name)
  }).flat()
  technos.value = [...new Set(technos.value)]

  types.value = new Set(projects.value.data.map(project => {
    return project.type
  }))

})

</script>

