<template>
    <div v-if="showPopup" class="success-popup">
      <i class="fa fa-check-circle" style="font-size:24px;color:white"></i>
      <p>{{ message }}</p>
    </div>
  </template>
  
  <script>
  export default {
    name: 'SuccessPopup',
    props: {
      message: {
        type: String,
        required: true
      }
    },
    data() {
        return {
          showPopup: false
        }
      },
      mounted() {
        this.showPopup = true;
        setTimeout(() => {
          this.showPopup = false;
        }, 2000);
      }
  }
  </script>
  
  <style scoped>
  .success-popup {
    text-align: center;
    background-color: green;
    color: white;
    padding: 10px 20px 10px 20px;
    border-radius: 10px;
    margin: -470px 0px -10px 1000px;
  }
  
  .success-popup i {
    font-size: 24px;
      /* margin-right: 100px 70px 0px 0px; */
  }
  </style>
  