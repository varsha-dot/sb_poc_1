<template>
    <!-- <button @click = "storyDetails">story-list</button> -->
    <div v-show="storyDisabled" v-if="storyList"><br /><br /><br /><br />
        <table class="table table-bordered">
        <thead style="color: black">
          <tr>
            <th scope="col"  style="text-align: left; width: 2%"> Id </th>
            <th scope="col"  style="text-align: left; width: 2%"> Name </th>
            <th scope="col"  style="text-align: left; width: 3%"> Description</th>
            <th scope="col"  style="text-align: left; width: 2%"> Type</th>
            <th scope="col"  style="text-align: left; width: 2%"> Priority </th>
            <th scope="col"  style="text-align: left; width: 2%;"> Delete </th>
          </tr>
        </thead>
        <tbody style="color:gainsboro">
          <tr v-for="list of storyList" :key="list.id" v-show="list.Type === 'story'"> 
                <td> {{ list.id }} </td>
                <td> {{ list.Name }} </td>
                <td> {{ list.Description }} </td>
                <td> {{ list.Type }} </td>
                <td> {{ list.Priority }} </td>
                <td> <a href="#" @click="deleteDetails(list.id)"> {{ deleteText }} </a> </td>
          </tr>
        </tbody>
      </table>
    </div>
</template>

<script>
import axios from 'axios'

    export default {
        data() {
            return {
                storyList: [],
                deleteText: "delete",
                storyDisabled: false,
            }
        },
        methods: {
            async getDetails() {
                const res = await fetch(" http://localhost:3000/details");
                const result = await res.json();
                console.log(result)
                this.storyList = result
             },
             deleteDetails(id) {
                axios.delete(`http://localhost:3000/details/${id}`);
                this.storyList = this.storyList.filter((list) => list.id !== id);
            },
            storyDetails() {
                this.storyDisabled = !this.storyDisabled
            }
        }, mounted() {
            this.getDetails();
        },
    }
</script>

<style scoped>
    a {
        color: black;
    }
    button {
    float: right;
    margin-right: 200px;
    margin-top: 30px;
    border: none;
    border-radius: 20px;
    padding: 10px 30px 10px 30px;
}

button:hover {
    background-color: palevioletred;
}
</style>