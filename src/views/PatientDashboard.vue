<template>
  <div class="container p-4 bg-gray-100">

   <!-- Full-width Navbar with rounded corners-->
   <nav class="flex justify-between items-center bg-green-700 px-4 py-4 mb-10 shadow-md w-full rounded-md">
      <h1 class="text-xl md:text-2xl ml-4 font-bold text-white">PharmaConnect</h1>
      <p class="text-l font-semibold text-white">Hello, {{patientName}}!</p>
      <button @click="goHome" class="bg-red-600 hover:bg-red-700 text-white font-bold py-2 px-4 rounded-lg">Logout</button>
    </nav>
    
<!-- Medication Schedule Section -->
<div class="mb-8 bg-white mx-12 lg:mx-36 rounded-xl shadow-lg">
  <h2 class="text-2xl font-semibold text-green-700 ml-8 pt-6">Your Medication Schedule</h2>
  <div class="p-6 grid grid-cols-1 lg:grid-cols-2 gap-4">
    <div v-for="medication in medications" :key="medication.id" class="mb-6 p-6 bg-gray-50 rounded-xl shadow border border-gray-200">
      <h3 class="text-lg font-semibold text-gray-800 mb-2">{{ medication.name }}</h3>
      <p class="text-gray-700 mb-2">Start Date: {{ medication.startDate }}</p>
      <p class="text-gray-700 mb-2">How to Take: {{ medication.howToTake }}</p>
      <p class="text-gray-700 mb-2">Frequency: {{ medication.frequency }}</p>
      <p class="text-gray-700 mb-2">Dosage: {{ medication.dosage }}</p>
      <p class="text-gray-700 mb-2">Notes: {{ medication.notes }}</p>
      <button @click="email" class="bg-blue-600 hover:bg-blue-700 text-white font-bold my-2 py-2 px-4 rounded-lg text-sm">View Side Effects</button>
    </div>
  </div>
</div>

<!-- Prescription Renewal Section -->
<div class="mb-8 bg-white mx-12 lg:mx-36 rounded-xl shadow-lg">
  <h2 class="text-2xl font-semibold mb-6 text-green-700 ml-8 pt-6">Your Active Prescriptions</h2>
  <div class="p-6 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
    <div v-for="prescription in prescriptions" :key="prescription.id" class="p-6 bg-gray-50 rounded-xl shadow border border-gray-200">
      <h3 class="text-lg font-semibold text-gray-800 mb-2">{{ prescription.medicationName }} ({{ prescription.dosage }})</h3>
      <p class="text-gray-700 mb-2">Prescription ID: {{ prescription.id }}</p>
      <p class="text-gray-700 mb-2">Renewal Status: {{ prescription.status }}</p>
      <button v-if="prescription.pending" @click="requestRenewal" class="bg-green-600 hover:bg-green-700 text-white font-bold my-2 py-2 px-4 rounded-lg text-sm">Request renewal</button>
      <p v-if="!prescription.pending" class="text-red-600 mb-2">Renewal not required.</p>
    </div>
  </div>
</div>


    <!-- Doctor Communication Section -->
    <div class="mb-8 bg-white mx-12 lg:mx-36 rounded-xl shadow-lg">
      <h2 class="text-2xl font-semibold mb-6 text-green-700 ml-8 pt-6">Doctor Messaging Service</h2>
      <div class="p-6">
        <!-- Individual Messages -->
        <div v-for="message in messages" :key="message.id" class="mb-6 p-6 bg-gray-50 rounded-xl shadow border border-gray-200">
          <p class="text-gray-800 mb-3 font-semibold">{{ message.doctorName }} ({{ message.timestamp }})</p>
          <p class="text-gray-700">{{ message.content }}</p>
        </div>

        <!-- Message Doctor Section -->
        <div class="mt-8 p-6 bg-gray-50 rounded-xl shadow border border-gray-200">
          <h3 class="text-lg font-semibold mb-4 text-green-700">Message Your Doctor</h3>
          <form @submit.prevent="sendMessage">
            <textarea v-model="newMessage" rows="4" class="border p-2 w-full rounded-lg mb-4" placeholder="Type your message here..."></textarea>
            <button type="submit" class="bg-green-600 hover:bg-green-700 text-white font-bold py-2 px-4 rounded-lg">Send Message</button>
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
        patientName: 'John Doe',
        medications: [
        { id: 1, name: 'Cipro', startDate: '2023-01-01', howToTake: 'Oral (tablets - do not chew)', frequency: 'Twice a day', dosage: '10mg', notes: 'Take anytime'},
        { id: 1, name: 'Insulin', startDate: '2023-01-01', howToTake: 'Intra Muscular (IM)', frequency: 'As needed', dosage: '25ml', notes: 'Take before meals'},
        { id: 1, name: 'Amoxicillin', startDate: '2023-01-01', howToTake: 'Oral (liquid)', frequency: 'Three times a day', dosage: '100mg', notes: 'Take after meals'},

          // Add more medications as needed
        ],
        prescriptions: [
          { id: 31412, name: 'Prescription 1', medicationName:'Insulin', dosage:'10mg x2', status: '6m prescription', pending:false },
          { id: 74123, name: 'Prescription 2', medicationName:'Paracetamol', dosage:'200mg x12', status: 'Pending', pending:true },
          { id: 74123, name: 'Prescription 3', medicationName:'Amoxicillin', dosage:'400mg x4', status: 'Pending', pending:true },
          { id: 74123, name: 'Prescription 4', medicationName:'Codeine', dosage:'75mg x10', status: 'Pending', pending:true },
        ],
        messages: [
          { id: 1, doctorName: 'Dr. Smith', timestamp: '9:37 AM', content: 'Hello, have you had any medication side effects?' },
          { id: 2, doctorName: 'Dr. Jones', timestamp: '2:45 PM', content: 'Please call when you are available to discuss your prescription for blood pressure medication.' },
      ],
        newMessage: ''
      };
    },
    methods: {
      sendMessage() {
        // Method to send message
                // Send message to doctor
          this.messages.push({
          id: this.messages.length + 1,
          doctorName: 'John Doe',
          timestamp: '13:00 PM',
          content: this.newMessage
        });
        this.newMessage = '';
      },
      email() {
        this.$notify({
          title: "We're sending you an email",
          text: "You will receive an email detailing your drug side effects shortly.",
          type: "success",
        });
      },
      requestRenewal() {
        this.$notify({
          title: "Request sent",
          text: "We have sent a request for renewal to your pharmacist. They will contact you soon!",
          type: "success",
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
  /* You can add custom styles here if needed */
  </style>
