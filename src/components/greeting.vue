<template>
    <section class="greeting">
      <h2 class="title">
        What's up, {{fullname}}!
      </h2>
    </section>
  </template>
  
  <script>

  export default {
    name: 'GreetingSection', // Use a multi-word component name
    props: ['firstname', 'lastname'],
    computed: {
        fullname(){
            return `${this.firstname} ${this.lastname}`
        },
    },
  };
  </script>
  