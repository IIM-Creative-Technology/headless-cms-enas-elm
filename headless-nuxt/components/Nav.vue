<template>
    <nav class="flex justify-between mb-10">
        <NuxtLink :to="`/`">
            Accueil
        </NuxtLink>
        <div class="flex gap-10">
            <NuxtLink :to="`/presentation`">
                Présentation
            </NuxtLink>
            <NuxtLink :to="`/projects`">
                Mes projets
            </NuxtLink>
        </div>
    </nav>
</template>

