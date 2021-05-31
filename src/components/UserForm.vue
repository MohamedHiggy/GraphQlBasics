<template>
    <form @submit.prevent="submit" class="shadow">
        <h1>Add user</h1>
        <div class="form-group">
            <label for="name">Name</label>
            <input type="text" class="form-control" id="name" placeholder="Name" v-model="name" required>
        </div>
        <div class="form-group">
            <label for="twitter">Twitter</label>
            <input type="text" class="form-control" id="twitter" placeholder="Twitter" v-model="twitter" required>
        </div>
        <div class="form-group">
            <label for="rocket">Choose Rocket</label>
            <select class="form-control" v-model="rocket" required id="rocket">
                <option :selected="true" :value="null">Choose Rocket</option>
                <option v-for="name in ['Falcon 1', 'Falcon 9', 'Falcon Heavy']" :key="name" :value="name">
                    {{name}}
                </option>
            </select>
        </div>
        <button type="submit" class="btn btn-primary">Submit</button>
    </form>
</template>

<script>
import uuidv4 from 'uuid/v4'
import { INSERT_USER } from "../mutations"
import { GET_USERS } from "../queries"
    export default {
        data(){
            return{
                name: '',
                twitter: '',
                rocket: ''
            }
        },
        methods: {
            submit() {
                const {name, twitter, rocket} = this.$data
                const id = uuidv4()
                this.$apollo.mutate({
                    mutation: INSERT_USER,
                    variables: {
                        id,
                        name,
                        twitter,
                        rocket
                    },
                    // new fetch data without loadint page
                    //refetchQueries: ['getUsers'],
                    update: (cache, {data: {insert_users} }) => {
                        const [newUser] = insert_users.returning;
                        const data = cache.readQuery({ query: GET_USERS});
                        data.users.unshift(newUser);
                        data.users.pop();
                        cache.writeQuery({ query: GET_USERS, data})
                    },
                    optimisticResponse: {
                        __typename: "Mutation",
                        insert_users: {
                            __typename: "users_mutation_response",
                            returning: [
                                {
                                    __typename: "users",
                                    id: -1,
                                    name,
                                    twitter,
                                    rocket
                                }
                            ]
                        }
                    }
                })
                .then(data => {
                    console.log("User added: ", data)
                })
                .catch(error => {
                    console.error(error)
                })
                .then(() => {
                        Object.assign(this.$data, {
                            name: "",
                            twitter: "",
                            rocket: ""
                        })
                    })
                }
            }
        }
</script>

<style lang="scss">
form {
    margin: 0 auto;
    border-radius: 10px;
    padding: 40px 20px;
}
</style>