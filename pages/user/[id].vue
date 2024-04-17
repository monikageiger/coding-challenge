<template>
    <article>
        <h1>User profile</h1>
        <p>Name: {{ data.name }}</p>
        <p>Email: {{ data.email }}</p>
        <p>Website: {{ data.website }}</p>
        <p>Phone number: {{ data.phone }}</p>
        <p v-if="data && data.company">Company name: {{ data.company.name }}</p>
    </article>
</template>

<script setup>
const { id } = useRoute().params

const { data, error } = await useFetch(
    `https://jsonplaceholder.typicode.com/users/${id}`
)
</script>

<style></style>
