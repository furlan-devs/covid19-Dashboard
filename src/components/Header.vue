<template>
    <header class="header">
      <div class="header-logo">
        <img src="../assets/vue.svg" alt="Logo">
        <h1 class="header-title">{{ title }}</h1>
      </div>

    </header>
  </template>
  
  <script>
  export default {
    name: 'Header',
    props: {
      title: {
        type: String,
        required: true
      }
    }
  }
  </script>
  
  <style>
  .header {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 1rem;
    background-color: #616e6d;
    color: #fff;
  }
  
  .header-logo {
    display: flex;
    align-items: center;
  }
  
  .header-logo img {
    margin-right: .5rem;
  }
  
  .header-title {
    font-size: 2.5rem;
    font-weight: bold;
  }
  
  </style>
  