// 代码生成时间: 2025-10-18 13:12:01
  import { onMount, writable } from 'svelte/store';

  // Health data store
  const healthData = writable({
    heartRate: 0,
    bloodPressure: { systolic: 0, diastolic: 0 },
    bodyTemperature: 0,
    steps: 0,
  });

  // Simulate receiving health data
  function receiveHealthData() {
    return {
      heartRate: Math.floor(Math.random() * 100) + 60,
      bloodPressure: {
        systolic: Math.floor(Math.random() * 20) + 100,
        diastolic: Math.floor(Math.random() * 10) + 60,
      },
      bodyTemperature: (Math.random() * 2 - 1) * 10 + 36.5,
      steps: Math.floor(Math.random() * 10000) + 1000,
    };
  }

  // Function to fetch health data
  function fetchHealthData() {
    healthData.set(receiveHealthData());
  }

  // Initialize data fetching
  onMount(() => {
    fetchHealthData();
    setInterval(fetchHealthData, 5000); // Update every 5 seconds
  });
</script>

<!-- UI to display health data -->
<div class="health-monitor">
  <h1>Health Monitor</h1>

  <div class="data-section">
    <h2>Heart Rate</h2>
    <p>{$healthData.heartRate} bpm</p>
  </div>

  <div class="data-section">
    <h2>Blood Pressure</h2>
    <p>{$healthData.bloodPressure.systolic}/{$healthData.bloodPressure.diastolic} mmHg</p>
  </div>

  <div class="data-section">
    <h2>Body Temperature</h2>
    <p>{$healthData.bodyTemperature}°C</p>
  </div>

  <div class="data-section">
    <h2>Steps</h2>
    <p>{$healthData.steps}</p>
  </div>
</div>

<style>
  .health-monitor {
    max-width: 400px;
    margin: auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 8px;
  }

  .data-section {
    margin-bottom: 20px;
  }
</style>