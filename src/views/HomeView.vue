<template>
  <div class="flex justify-center items-center h-screen bg-gray-100">
    <div class="p-10 bg-white rounded-lg shadow-xl mx-36">
      <h1 class="text-2xl text-green-700 font-bold mb-6">Welcome to PharmaConnect</h1>

      <p>A HCI Project by Conor Fleming, Evan Murphy, and Michael Gill</p> <br>
      <p> This page is a prototype homepage only, and is used to make navigating our prototype easier, so you can experience the dashboards
        that are available to both types of users; patients and pharmacists.
      </p> <br>
      <p> We did not implement backend functionality. This page is buit using Vue3 and TailwindCSS, using Javascript in client-side capacity only.</p>
      
      <br> 

      <div class="space-y-4">
        <button @click="goToPage('dashboardp')" class="w-full bg-green-600 text-white font-bold py-3 px-6 rounded-lg hover:bg-green-700 transition-colors">Patient Dashboard</button>
        <button @click="goToPage('pharmacy')" class="w-full bg-green-600 text-white font-bold py-3 px-6 rounded-lg hover:bg-green-700 transition-colors">Pharmacist Dashboard</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomePage',
  methods: {
    goToPage(pageName) {
      this.$router.push({ name: pageName });
      console.log('Navigating to:', pageName);
    }
  }
};
</script>

<style scoped>
/* You can add custom styles here if needed */
</style>
