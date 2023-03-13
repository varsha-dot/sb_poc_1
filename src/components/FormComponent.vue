<template>
    <div class="container">
        <div>
            <pre>
                {{ JSON.stringify(formValues, null, 2) }}
            </pre>
        </div>
             <form @submit.prevent="addItem" v-show="formDisabled"> 
                <fieldset>
                    <h4>Enter the details</h4><br/>
                    <div id="name">
                        <label for = "Fname">Name: </label>
                        <input type="text" id="Fname" v-model="name" ><br /><br />
                    </div>

                    <div id="description">
                        <label for = "desc">Description: </label>
                        <textarea id="desc" v-model="description"> </textarea><br /><br />
                    </div>

                    <div id="type">
                        <label for="Type">Type: </label>
                        <select id="Type" v-model="type">
                            <option value="">Select Type</option>
                            <option value="story">Story</option>
                            <option value="bug">Bug</option>
                        </select><br /><br />
                    </div>

                    <div id="priority">
                        <label>Priority: </label>
                        <input type="radio" id="high" value="high" v-model="priority" />
                        <label for="html"> High</label>
                        <input type="radio" id="medium" value="medium" v-model="priority" />
                        <label for="css">Medium</label>
                        <input type="radio" id="low" value="low" v-model="priority" />
                        <label for="js">Low</label>
                    </div><br />
                        <button type="submit" :disabled="!isFormValid" @click="formDetails()">Save details</button>
                </fieldset>
            </form>
            <!-- <success-popup v-if="success" message="Details saved successfully" /> -->
            <!-- <div v-if="showSuccessMessage" id="success">
                <p>Item added successfully!</p>
            </div> -->
    </div>    
</template>

<script>
  import axios from "axios"
  //import SuccessPopup from './SuccessPopup.vue'

    export default {
        // components: {
        //     SuccessPopup
        // },
        data() {
            return {
                details: [],
                name: "",
                description: "",
                type: "",
                priority: "",
                formDisabled: true,
                showSuccessMessage: false,
                dialog: false,
                // success: false
            }
        },
        computed: {
            isFormValid() {
                return this.name && this.description && this.type && this.priority;
            },
        },
        methods: {
            async getDetails() {
                const res = await fetch(" http://localhost:3000/details");
                const result = await res.json();
                console.log(result)
                this.details = result
             },
            async addItem() {
                const res = await axios.post("http://localhost:3000/details", {
                    Name: this.name,
                    Description: this.description,
                    Type: this.type,
                    Priority: this.priority
                });
                    this.details = [...this.details, res.data]
                    this.name = "";
                    this.description = "";
                    this.type = "";
                    this.priority = "";
                    this.showSuccessMessage = true;
                    this.success = true
            },

            formDetails() {
                this.formDisabled = !this.formDisabled
            },

            showAlert() {
                alert("Details added successfully")
            }

        }, mounted() {
             this.getDetails();
        },
    }
</script>
  
  <style scoped>

#task_details {
    text-align: center;
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

fieldset {
    background-color: white;
    margin: 100px 400px 50px 400px;
    border-radius: 10px;
    /* text-align: left; */
    padding: 30px 0px 30px 85px;
}

.flex-container {
  display: flex;
}

.flex-container > div {
  margin: 10px 150px 0px 350px;
  padding: 20px;
}

h4 {
    margin-left:60px;
}


input[type = text] {
    border-radius: 4rem;
}

#Fname {
    margin-left: 70px;
}
#desc{
    margin-left: 35px;
}

#Type {
    margin-left: 80px;
}

#high {
    margin-right: 8px;
    margin-left: 65px;
}

#medium {
    margin-right: 8px;
    margin-left: 10px;
}

#low {
    margin-right: 8px;
    margin-left: 10px;
}

#success {
    background-color:white;
    color: green;
    padding: 20px 30px 20px 30px;
    margin: 100px 100px 0px 300px; 
    text-align: center;
    font-size: 24px;
    font-weight: bold;
    border-radius: 10%;
}

</style>