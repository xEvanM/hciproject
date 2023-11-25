<template>
    <div class="container p-4 bg-gray-100">
      <!-- Full-width Navbar with rounded corners -->
      <nav class="flex justify-between items-center bg-blue-700 px-4 py-4 mb-10 shadow-md w-full rounded-md">
        <h1 class="text-xl md:text-2xl ml-4 font-bold text-white">PharmaConnect</h1>
        <p class="text-l font-semibold text-white">Hello, {{ pharmacistName }} <i>(Pharmacy Mode)</i></p>
        <button @click="goHome" class="bg-red-600 hover:bg-red-700 text-white font-bold py-2 px-4 rounded-lg">Logout</button>
      </nav>
  
      <!-- Prescription Renewal Request Section -->
      <div class="mb-8 bg-white mx-12 lg:mx-36 rounded-xl shadow-lg">
        <h2 class="text-2xl font-semibold text-blue-700 ml-8 pt-6">Prescription Renewal Requests</h2>
        <div class="p-6 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
          <div v-for="request in renewalRequests" :key="request.id">
            <div class="p-6 bg-gray-50 rounded-xl shadow border border-gray-200" >
            <h3 class="text-lg font-semibold text-gray-800 mb-2">{{ request.patientName }} ({{ request.medicationName }})</h3>
            <p class="text-gray-700 mb-2">Request ID: {{ request.id }}</p>
            <p class="text-gray-700 mb-2">Requested On: {{ request.dateRequested }}</p>
            <p class="text-gray-700 mb-2">Status: {{ request.status }}</p>
            <button @click="acceptRenewal(request.id)" class="bg-green-600 hover:bg-green-700 text-white font-bold my-2 mr-1 py-2 px-4 rounded-lg text-sm">Approve</button>
            <button @click="denyRenewal(request.id)" class="bg-red-600 hover:bg-red-700 text-white font-bold my-2 py-2 ml-1 px-4 rounded-lg text-sm">Decline</button>
        </div>
        </div>
        </div>
      </div>
  
      <!-- Doctor Communication Section -->
      <div class="mb-8 bg-white mx-12 lg:mx-36 rounded-xl shadow-lg">
        <h2 class="text-2xl font-semibold mb-6 text-blue-700 ml-8 pt-6">Doctor Messaging</h2>
        <div class="p-6">
          <!-- Individual Messages -->
          <div v-for="message in messages" :key="message.id" class="mb-6 p-6 bg-gray-50 rounded-xl shadow border border-gray-200">
            <p class="text-gray-800 mb-3 font-semibold">{{ message.doctorName }} ({{ message.timestamp }})</p>
            <p class="text-gray-700">{{ message.content }}</p>
          </div>
  
          <!-- Message Doctor Section -->
          <div class="mt-8 p-6 bg-gray-50 rounded-xl shadow border border-gray-200">
            <h3 class="text-lg font-semibold mb-4 text-blue-700">Doctor Messaging Service</h3>
            <form @submit.prevent="sendMessage">
              <textarea v-model="newMessage" rows="4" class="border p-2 w-full rounded-lg mb-4" placeholder="Type your message here..."></textarea>
              <button type="submit" class="bg-blue-600 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-lg">Send Message</button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'PharmacistDashboard',
    data() {
      return {
        pharmacistName: 'Alex Johnson',
        renewalRequests: [
          { id: 101, patientName: 'Jane Doe', medicationName: 'Amoxicillin', dateRequested: '2023-11-01', status: 'Pending', isVisible: true },
          { id: 102, patientName: 'John Smith', medicationName: 'Metformin', dateRequested: '2023-11-03', status: 'Pending', isVisible: true },
          { id: 103, patientName: 'Emily Davis', medicationName: 'Lisinopril', dateRequested: '2023-11-05', status: 'Pending', isVisible: true },
          // Additional sample requests can be added here
        ],
        finishedRequests: [],
        messages: [
          { id: 1, doctorName: 'Dr. Brown', timestamp: '9:00 AM', content: 'Please confirm the dosage for John Smith’s Metformin prescription.' },
          { id: 2, doctorName: 'Dr. Wilson', timestamp: '11:30 AM', content: 'Emily Davis reported side effects. Consider a medication switch.' },
          // Additional sample messages can be added here
        ],
        newMessage: ''
      };
    },
    methods: {
      sendMessage() {
        // Send message to doctor
        this.messages.push({
          id: this.messages.length + 1,
          doctorName: 'Alex Johnson',
          timestamp: '12:00 PM',
          content: this.newMessage
        });
        this.newMessage = '';
      },
      acceptRenewal(requestId) {
        const requestIndex = this.renewalRequests.findIndex(request => request.id === requestId);
        if (requestIndex !== -1) {
            const finishedRequest = { ...this.renewalRequests[requestIndex], status: 'Allowed' };
            this.finishedRequests.push(finishedRequest);
            this.renewalRequests.splice(requestIndex, 1);
        }
        this.$notify({
          title: "Prescription Updated",
          text: "Prescription has been renewed!",
          type: "success",
        });
      },
      denyRenewal(requestId) {
        const requestIndex = this.renewalRequests.findIndex(request => request.id === requestId);
        if (requestIndex !== -1) {
            const finishedRequest = { ...this.renewalRequests[requestIndex], status: 'Declined' };
            this.finishedRequests.push(finishedRequest);
            this.renewalRequests.splice(requestIndex, 1);
        }
        this.$notify({
          title: "Prescription Updated",
          text: "Prescription renewal declined.",
          type: "error",
        });
      },
      goHome() {
       // push to home path '/'
       this.$router.push('/');
      }
    }
    };
  </script>
  
  <style scoped>
  /* Custom styles can be added here */
  </style>
  