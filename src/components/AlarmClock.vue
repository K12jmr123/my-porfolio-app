<!-- components/AlarmClock.vue -->
<template>
  <div class="alarm-clock">
    <div class="display">
      {{ time }}
    </div>
    <div class="controls">
      <input type="time" v-model="alarmTime" ref="timeInput" />
      <button @click="setAlarm">Set Alarm</button>
    </div>
  </div>
</template>
  
  <script>
  import anime from 'animejs';
  
  export default {
    data() {
      return {
        alarmTime: '00:00',
        time: this.getCurrentTime(),
        isAlarmSet: false,
        alarmSound: new Audio(require('@/sounds/alarm.wav')), // Adjust the path as needed
      };
    },
    methods: {
      getCurrentTime() {
        const now = new Date();
        const hours = now.getHours().toString().padStart(2, '0');
        const minutes = now.getMinutes().toString().padStart(2, '0');
        return `${hours}:${minutes}`;
      },
      updateTime() {
        this.time = this.getCurrentTime();
        if (this.isAlarmSet && this.time === this.alarmTime) {
          this.triggerAlarm();
        }
      },
      setAlarm() {
        this.isAlarmSet = true;
      },
      triggerAlarm() {
      this.alarmSound.play(); // Play the alarm sound
      anime({
        targets: '.alarm-clock',
        backgroundColor: '#e74c3c',
        duration: 2000,
        loop: 4,
        direction: 'alternate',
        easing: 'easeInOutQuad',
      });
      setTimeout(() => {
        this.isAlarmSet = false;
        this.$refs.timeInput.blur();
        this.alarmSound.pause(); // Pause the sound after a certain time (adjust as needed)
      }, 8000);
    },
  },
    mounted() {
      setInterval(this.updateTime, 1000);
    },
  };
  </script>
  
  <style scoped>
  .alarm-clock {
    max-width: 300px;
    margin: auto;
    padding: 20px;
    background-color: #3498db;
    border-radius: 10px;
  }
  
  .display {
    font-size: 1.5em;
    margin-bottom: 20px;
  }
  
  .controls {
    display: flex;
    align-items: center;
  }
  
  input {
    margin-right: 10px;
  }
  </style>
  