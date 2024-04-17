<template>
    <AwesomeSection>
        <h2>Users List</h2>
        <input type="text" placeholder="Search..." v-model="search" />
        <ul v-for="user in filteredUsers" :key="user.id">
            <NuxtLink :to="`/user/${user.id}`" tag="li">
                <p>Name: {{ user.name }}</p>
                <p>Email: {{ user.email }}</p>
                <p>Username: {{ user.username }}</p>
                <hr />
            </NuxtLink>
        </ul>
    </AwesomeSection>
</template>

<!-- USE WHEN SSR -->
<script setup>
import { useAsyncData } from 'nuxt/app'

const search = ref('')

const filteredUsers = computed(() =>
    users
        ? users.value.filter((user) =>
              user.name.toLowerCase().includes(search.value.toLowerCase())
          )
        : []
)

const { data: users } = useAsyncData(() =>
    fetch('https://jsonplaceholder.typicode.com/users').then((res) =>
        res.json()
    )
)
</script>


<!-- USE WHEN CLIENT SIDE RENDERING -->

<!--
<script setup>
import { ref, computed, onMounted } from 'vue'

let users = ref([])
const search = ref('')

const filteredUsers = computed(() =>
    users.value.filter((user) =>
        user.name.toLowerCase().includes(search.value.toLowerCase())
    )
)

onMounted(async () => {
    const response = await fetch('https://jsonplaceholder.typicode.com/users')
    users.value = await response.json()
})
</script> -->
