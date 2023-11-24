<template>
  <div class="container mx-auto p-4 bg-gray-100">
    <h1 class="text-2xl font-bold text-center mb-4 text-green-700">Patient Dashboard</h1>
    
    <!-- Medication Schedule Section -->
    <div class="mb-6 p-4 mx-24 bg-white rounded-lg shadow">
      <h2 class="text-xl font-semibold mb-2 text-green-700">Today's Medication Schedule</h2>
      <div>
        <div v-for="medication in medications" :key="medication.id" class="mb-2">
          <p class="text-gray-600"><strong>{{ medication.name }}:</strong> {{ medication.dosage }} at {{ medication.time }}</p>
        </div>
      </div>
    </div>
    
    <!-- Prescription Renewal Section -->
    <div class="mb-6 bg-white mx-24 rounded-lg shadow">
      <h2 class="text-xl font-semibold mb-2 text-green-700 p-4">Prescription Renewals</h2>
      <div>
        <div v-for="prescription in prescriptions" :key="prescription.id" class="mb-2 p-4 border-b last:border-b-0">
          <p class="text-gray-600">{{ prescription.name }} - Renewal Status: {{ prescription.status }}</p>
          <button class="bg-green-500 hover:bg-green-600 text-white font-bold py-1 px-3 rounded text-sm">Request renewal</button>
        </div>
      </div>
    </div>
    
    <!-- Doctor Communication Section -->
    <div class="mb-6 bg-white mx-24 rounded-lg shadow">
      <h2 class="text-xl font-semibold mb-2 text-green-700 p-4">Messages from Your Doctor</h2>
      <div class="p-4">
        <div v-for="message in messages" :key="message.id" class="mb-2 p-2 bg-gray-100 rounded">
          <p class="text-gray-600"><strong>{{ message.doctorName }}</strong> ({{ message.timestamp }}): {{ message.content }}</p>
        </div>
        <!-- Message Doctor Section -->
        <div class="mt-4 p-4 bg-white rounded-lg">
          <h3 class="text-lg font-semibold mb-2 text-green-700">Message Your Doctor</h3>
          <form @submit.prevent="sendMessage">
            <textarea v-model="newMessage" rows="4" class="border p-2 w-full rounded" placeholder="Type your message here..."></textarea>
            <button type="submit" class="mt-2 bg-sage-600 hover:bg-sage-700 text-white font-bold py-2 px-4 rounded">
              Send Message
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PatientDashboard',
  data() {
    return {
      medications: [
        { id: 1, name: 'Medication 1', dosage: '100mg', time: '8:00 AM' },
        // Add more medications as needed
      ],
      prescriptions: [
        { id: 1, name: 'Prescription 1', status: 'Pending' },
        { id: 2, name: 'Prescription 2', status: '2 months remaining' },
        // Add more prescriptions as needed
      ],
      messages: [
        { id: 1, content: 'Dont forget your check-up tomorrow!', doctorName: 'Dr. Smith', timestamp: '3:00PM 18/10/2023' },
        // Add more messages as needed
      ],
    };
  },
  methods: {
    sendMessage() {
      // Method to send message
    }
  }
};
</script>

<style scoped>
/* You can add custom styles here if needed */
</style>
