<template>
  <q-layout view="hHh lpR fFf">

    <q-header elevated class="bg-primary text-white">
      <q-toolbar>
        <q-toolbar-title>
            <strong>
              Ciervo Cafe Warehouse
            </strong>
        </q-toolbar-title>

        <q-btn flat round dense icon="home" @click="$router.push('/')">
          <q-tooltip>
            Home
          </q-tooltip>
        </q-btn>

        <q-btn flat round dense icon="storm" @click="$router.push('/report')">
          <q-tooltip>
            Report
          </q-tooltip>
        </q-btn>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <!-- <q-card flat bordered>
        <div class=""><strong>Humidity Normal Rating:<q-separator></q-separator>50-70%</strong></div>
        <q-separator></q-separator>
        <div class=""><strong>Temperature Normal Rating:<q-separator></q-separator>40-59°C</strong></div>
      </q-card> -->
      <router-view />
    </q-page-container>

  </q-layout>
</template>
<script>
export default {
  methods: {
    sendRequest() {
      // Code to send request to your server
      // You can use Axios or fetch API for making HTTP requests
      // Example using Axios:
      axios.get('http://localhost:4444/generate_report', { data:'temperature_data' })
        .then(response => {
          console.log('Server response:', response.data);
          // Handle response data as needed
        })
        .catch(error => {
          console.error('Error sending request:', error);
          // Handle error
        });
    }
  }
}

</script>

