<template>
    <article>
        <h2>User profile</h2>
        <div v-if="data">
            <p>Name: {{ data.name }}</p>
            <p>Email: {{ data.email }}</p>
            <p>Website: {{ data.website }}</p>
            <p>Phone number: {{ data.phone }}</p>
            <p v-if="data && data.company">
                Company name: {{ data.company.name }}
            </p>
        </div>
        <p v-if="error">An error occurred: {{ error.message }}</p>
    </article>
</template>

<script setup>
const { id } = useRoute().params

const { data, error } = await useFetch(
    `https://jsonplaceholder.typicode.com/users/${id}`
)
</script>

<style></style>
