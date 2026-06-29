<template>
  <div class="home">
    
    <input type="text" v-model="firstname" placeholder="Enter your firstname" />
    <input type="text" v-model="lastname" placeholder="Enter your lastname" />
    <GreetingSection :firstname="firstname" :lastname="lastname" />

  </div>
<div>
 <h2 class="title"> welcome to our home page</h2>
</div>


</template>

<script>
// @ is an alias to /src
import GreetingSection from '../components/greeting.vue';
import { ref } from 'vue';
export default {
  name: 'HomeView',
  components: {
    GreetingSection,
  },
  setup(){
    const firstname = ref('')
    const lastname = ref('')
    return {
      firstname,
      lastname,
    }
  }
}
</script>
