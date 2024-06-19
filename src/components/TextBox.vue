
<template>
  <div>
    <label for="inputText">Enter text:</label>
    <div class="input-container">
      <input id="inputText" type="text" v-model="inputText">
      <button @click="addText">Add</button>
    </div>
    <div class="output-box" v-if="submittedTextArray.length > 0">
      <p>Text entered:</p>
      <div class="text-container">
        <div v-for="(text, index) in submittedTextArray" :key="index" class="text-entry">
          <div v-if="editIndex !== index" class="text-content">
            <p>{{ text }}</p>
            <div class="actions">
              <span @click="confirmDelete(index)">❌</span>
              <span @click="startEdit(index)">✏️</span>
            </div>
          </div>
          <div v-else>
            <input type="text" v-model="editedText" @keyup.enter="saveEdit(index)" @keyup.esc="cancelEdit">
            <button @click="saveEdit(index)">Save</button>
            <button @click="cancelEdit">Cancel</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputText: '',
      submittedTextArray: [],
      editIndex: -1,
      editedText: ''
    };
  },
  methods: {
    addText() {
      if (this.inputText.trim() !== '') {
        this.submittedTextArray.push(this.inputText);
        this.inputText = ''; // Clear the input after adding text
      }
    },
    confirmDelete(index) {
      if (confirm(`Are you sure you want to delete "${this.submittedTextArray[index]}"?`)) {
        this.deleteText(index);
      }
    },
    deleteText(index) {
      this.submittedTextArray.splice(index, 1);
    },
    startEdit(index) {
      this.editIndex = index;
      this.editedText = this.submittedTextArray[index];
    },
    saveEdit(index) {
      if (this.editedText.trim() !== '') {
        this.submittedTextArray[index] = this.editedText;
        this.cancelEdit();
      }
    },
    cancelEdit() {
      this.editIndex = -1;
      this.editedText = '';
    }
  }
};
</script>

<style scoped>
.input-container {
  display: flex;
  align-items: center;
  gap: 10px; 
}

.output-box {
  margin-top: 20px; /* Increase the margin between input and output */
}

.text-container {
  border: 1px solid #ccc;
  padding: 10px;
}

.text-entry {
  border-bottom: 1px solid #ccc;
  padding: 10px 0;
}

.text-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.actions span {
  cursor: pointer;
  margin-left: 5px;
}

.actions span:hover {
  color: red; /* Change color on hover for better UX */
}

.text-entry input[type="text"] {
  width: calc(100% - 140px); 
  margin-right: 10px;
}

.text-entry button {
  margin-right: 5px;
}
</style>
