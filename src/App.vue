<script setup>
// import HomeView from './views/HomeView.vue';

import { RouterLink, RouterView } from 'vue-router'
// import HelloWorld from './components/HelloWorld.vue'

</script>

<template>
  <header >
    <nav>
      <div class='w-full py-3 border-b'>

        <div class='flex justify-between px-20 items-center font-semibold'>
          <div>
            <h1 class="text-2xl">MTIX-ID</h1>
          </div>
          <div class='flex xl:gap-10 md:gap-8  gap-2'>
            <RouterLink to="/">Home</RouterLink>
            <RouterLink to="/about">About</RouterLink>
          </div>
          <div>
            <button class='py-2 px-6 bg-black text-white rounded-3xl font-semibold'>Login</button>
          </div>
        </div>
        
      </div>
    </nav>
    
  </header>

  <RouterView />

  <!-- <HomeView/> -->
</template>

<style scoped>

</style>
