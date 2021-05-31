<template>
    <ul>
        <li v-for="rocket in rockets" :key="rocket.id">
            <h1>{{rocket.name}}</h1>
            <p>{{rocket.description}}</p>
            <p>{{rocket.constPerLaunc}}</p>
        </li>
    </ul>
</template>

<script>
import gql from 'graphql-tag'
const query = gql`
query getRockets {
    rockets {
        id
        name
        description
        constPerLaunc: cost_per_launch
    }
}
`
export default {
    apollo: {
        rockets: {
            query
        }
    }
}
</script>

<style lang="scss" scoped>

</style>