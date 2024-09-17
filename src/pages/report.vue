<template>
  <q-page class="flex flex-center">
    <div class="row justify-center">
      <q-btn color="primary" label="Generate Report" @click="generateReport"/>

      <q-card flat  class="temp-card q-ml-md">
        <q-card-section class="q-pa-none">
            <div class="temp-info">
              <q-list bordered separator>
                <q-separator spaced />
                <q-card-section><q-item-label header class="row justify-center"><strong>Report:</strong></q-item-label></q-card-section>

                <q-item v-for="(record, index) in dailyReportData" :key="index" v-ripple>

                  <q-item-section>
                    <q-item-label class="text-primary">Highest Humidity: {{ record.highest_humidity }}</q-item-label>
                    <q-item-label class="text-red"> Highest Temperature: {{ record.highest_temperature }}</q-item-label>

                    <q-item-label class="text-primary">Lowest Humidity: {{ record.lowest_humidity }}</q-item-label>
                    <q-item-label class="text-red"> Lowest Temperature:  {{ record.lowest_temperature }}</q-item-label>
                  </q-item-section>

                  <q-item-section side top>
                    <q-item-label caption>Id: {{record.id}}</q-item-label>
                    <!-- <q-item-label caption>Time: {{record.createdat}}</q-item-label> -->
                    <!-- <q-icon name="ac_unit" color="primary" /> -->
                  </q-item-section>
                </q-item>
              </q-list>
            </div>
        </q-card-section>
      </q-card>
      <!-- reports -->

    </div>
  </q-page>
</template>

<script>
import { defineComponent, ref, onMounted } from 'vue';
import axios from 'axios';



export default defineComponent({
  name: 'Report',
  setup() {
    const temperatureData = ref([]);
    const dailyReportData = ref([]);

    const generateReport = async () => {
      try {
        const response = await axios.get('http://localhost:4444/generate_report');
        dailyReportData.value = response.data;
      } catch (error) {
        console.error('Error fetching report', error);
      }
    };

    return {
      generateReport,
      dailyReportData
    };
  },
});


</script>



<style scoped>
.temp-card {
  width: 450px;
  border-radius: 16px;
  background-color: #fff;
}
.temp-card2 {
  width: 600px;
  border-radius: 16px;
  background-color: #fff;
}
.temp-info {
  /* max-height and overflow-y for scrollable content */
  max-height: 400px;
  overflow-y: auto;
}
.weather-widget {
  background-color: #f5f5f5;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
.weather-card {
  width: 300px;
  height: 400px;
  border-radius: 16px;
  background-color: #fff;
}
.weather-header {
  display: flex;
  justify-content: space-between;
  padding: 16px;
}
.weather-content {
  text-align: center;
  padding: 16px;
}
.time-location {
  margin-bottom: 16px;
}
.time {
  font-size: 24px;
  font-weight: bold;
}
.location {
  color: #888;
}
.weather-info {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.temperature {
  font-size: 48px;
  font-weight: bold;
  margin-top: 8px;
}
.weather-footer {
  display: flex;
  justify-content: space-around;
}
</style>
