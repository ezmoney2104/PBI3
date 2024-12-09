<template>
  <div 
    class="excel-cell" 
    :class="backgroundClass"
  >
    <label v-if="label" class="cell-label">{{ label }}</label>
    <span v-if="value" class="cell-value">{{ value }}</span>
    <input
      v-if="editable"
      v-model="inputValue"
      :placeholder="placeholder"
      class="cell-input"
      type="text"
    />
  </div>
</template>

<script>
export default {
  name: 'ExcelCell',
  props: {
    label: {
      type: String,
      required: false,
    },
    value: {
      type: String,
      required: false,
    },
    editable: {
      type: Boolean,
      default: true,
    },
    placeholder: {
      type: String,
      required: false,
    },
    errorCode: {
      type: Number,
      required: false,
      default: 0, // Default: No error code, no color change
    },
  },
  data() {
    return {
      inputValue: this.value || '',
    }
  },
  computed: {
    backgroundClass() {
      switch (this.errorCode) {
        case 1:
          return 'bg-green'
        case 2:
          return 'bg-yellow-green'
        case 3:
          return 'bg-red'
        default:
          return ''
      }
    },
  },
  watch: {
    inputValue(newValue) {
      this.$emit('update:value', newValue)
    },
  },
}
</script>

<style scoped>
.excel-cell {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  width: 150px;
  height: 100px;
  border: 1px solid #ddd;
  padding: 10px;
  box-sizing: border-box;
  background-color: #f9f9f9; /* Default background */
  transition: background-color 0.3s ease-in-out;
}

.cell-label {
  font-weight: bold;
  font-size: 14px;
  margin-bottom: 5px;
}

.cell-value {
  font-size: 14px;
  color: #555;
  margin-bottom: 5px;
}

.cell-input {
  width: 100%;
  border: 1px solid #ccc;
  padding: 8px;
  box-sizing: border-box;
  font-size: 14px;
  background-color: #fff;
}

.cell-input:focus {
  border-color: #2196f3;
  outline: none;
}

/* Dynamic background colors based on error codes */
.bg-green {
  background-color: #4caf50 !important; /* Green */
  color: #fff;
}

.bg-yellow-green {
  background-color: #9acd32 !important; /* Yellow-Green */
  color: #000;
}

.bg-red {
  background-color: #f44336 !important; /* Red */
  color: #fff;
}
</style>




----

<template>
  <div class="home-view">
    <h1>Vue Excel-like Application</h1>
    
    <!-- Error Code Selector -->
    <div class="error-code-selector">
      <label>Select Error Code for Left Cell:</label>
      <select v-model="leftCellErrorCode">
        <option value="1">Error 1 (Green)</option>
        <option value="2">Error 2 (Yellow-Green)</option>
        <option value="3">Error 3 (Red)</option>
      </select>
    </div>

    <!-- Excel Cells Side by Side -->
    <div class="excel-container">
      <!-- Left Cell (changes color based on errorCode) -->
      <ExcelCell 
        label="稼働状況" 
        value="稼働中" 
        :editable="false" 
        :errorCode="leftCellErrorCode" 
      />
      
      <!-- Right Cell -->
      <ExcelCell 
        label="右側のセル" 
        placeholder="Type something here..." 
        v-model="rightCellValue" 
      />
    </div>
  </div>
</template>

<script>
import ExcelCell from '@/components/ExcelCell.vue'

export default {
  name: 'HomeView',
  components: {
    ExcelCell,
  },
  data() {
    return {
      rightCellValue: '', // Value for the right-side cell
      leftCellErrorCode: 1, // Default error code for left cell
    }
  },
}
</script>

<style scoped>
.home-view {
  padding: 20px;
}

h1 {
  text-align: center;
  margin-bottom: 20px;
}

.excel-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  max-width: 400px;
  margin: 0 auto;
}

.excel-container > * {
  margin-right: 10px;
}

.excel-container > *:last-child {
  margin-right: 0;
}

.error-code-selector {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 20px;
}

.error-code-selector label {
  font-size: 16px;
  margin-right: 10px;
}

.error-code-selector select {
  font-size: 16px;
  padding: 5px 10px;
}
</style>
