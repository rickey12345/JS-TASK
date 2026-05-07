<template>
  <div class="container">
    <h1>📅 Daily Timetable</h1>

    <div v-for="(day, index) in schedule" :key="index" class="card">
      
      <!-- Clickable Day -->
      <div class="day-header" @click="toggle(index)">
        {{ day.name }}
        <span>{{ activeIndex === index ? "▲" : "▼" }}</span>
      </div>

      <!-- Modules with TIME -->
      <ul v-if="activeIndex === index" class="modules">
        <li
          v-for="(module, i) in day.modules"
          :key="i"
          :class="getClass(module)"
        >
          <span class="time">{{ times[i] }}</span>
          <span class="module">{{ module }}</span>
        </li>
      </ul>

    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeIndex: null,

      // ⏰ time slots
      times: [
        "08:00 - 09:00",
        "09:00 - 10:00",
        "10:00 - 10:20",
        "10:20 - 11:20",
        "11:20 - 12:20",
        "12:20 - 13:00",
        "13:00 - 14:00",
        "14:00 - 15:00",
        "15:00 - 15:20",
        "15:20 - 16:20",
        "16:20 - 17:20"
      ],

      schedule: [
        {
          name: "Monday",
          modules: ["UI/UX", "UI/UX", "BREAK", "DJF", "DJF", "LUNCH", "MATH", "MATH", "BREAK", "GD", "GD"]
        },
        {
          name: "Tuesday",
          modules: ["DJF", "DJF", "BREAK", "DJF Pract", "DJF Pract", "LUNCH", "CL", "CL", "BREAK", "VC Pract", "VC Pract"]
        },
        {
          name: "Wednesday",
          modules: ["VC", "VC", "BREAK", "DGV", "DGV", "LUNCH", "BREAK", "MATH", "MATH"]
        },
        {
          name: "Thursday",
          modules: ["UI/UX", "UI/UX", "BREAK", "DJF", "DJF Pract", "LUNCH", "PHY", "PHY", "BREAK", "DJF Pract", "DJF Pract"]
        },
        {
          name: "Friday",
          modules: ["DGV", "DGV", "BREAK", "FR", "FR", "LUNCH", "BREAK"]
        }
      ]
    }
  },

  methods: {
    toggle(index) {
      this.activeIndex = this.activeIndex === index ? null : index
    },

    getClass(module) {
      if (module === "BREAK") return "break"
      if (module === "LUNCH") return "lunch"
      return "normal"
    }
  }
}
</script>

<style>
.container {
  max-width: 650px;
  margin: auto;
  font-family: Arial;
}

h1 {
  text-align: center;
}

/* card */
.card {
  border: 1px solid #ccc;
  margin: 10px 0;
  border-radius: 8px;
  overflow: hidden;
}

/* header */
.day-header {
  background: #333;
  color: white;
  padding: 10px;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
}

/* list */
.modules {
  list-style: none;
  padding: 0;
  margin: 0;
}

.modules li {
  display: flex;
  justify-content: space-between;
  padding: 8px;
  border-bottom: 1px solid #eee;
}

/* time + module */
.time {
  font-weight: bold;
  color: #555;
}

.module {
  text-align: right;
}

/* special styles */
.break {
  background: orange;
  color: white;
  font-weight: bold;
}

.lunch {
  background: green;
  color: white;
  font-weight: bold;
}

.normal {
  color: black;
}
</style>