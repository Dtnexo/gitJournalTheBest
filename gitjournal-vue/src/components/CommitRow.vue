<script setup>
defineProps({
  commit: Object,
});
const emit = defineEmits(["update"]);

// Quand on modifie, on remonte l'info au parent
const onUpdate = () => {
  emit("update");
};
</script>

<template>
  <div class="commit-row">
    <div class="time-col">
      <div class="time">{{ commit.timeStr }}</div>
      <div class="duration-wrapper">
        <input
          type="number"
          v-model.number="commit.duration"
          @input="onUpdate"
          class="edit-duration"
          min="0"
        />
        <span class="min-label">min</span>
      </div>
    </div>

    <div class="content-col">
      <div class="msg-container">
        <span v-if="commit.status" :class="['status-badge', commit.status]">
          {{ commit.status }}
        </span>
        <input
          v-model="commit.message"
          @input="onUpdate"
          class="edit-message"
        />
      </div>
    </div>
  </div>
</template>

<style scoped>
.commit-row {
  display: flex;
  margin-bottom: 12px;
  align-items: center;
}
.time-col {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  margin-right: 15px;
  min-width: 70px;
}
.time {
  font-weight: bold;
  color: #35495e;
  font-size: 0.9em;
  margin-bottom: 2px;
}
.content-col {
  flex: 1;
  border-left: 2px solid #f0f0f0;
  padding-left: 15px;
}
.msg-container {
  display: flex;
  align-items: center;
  gap: 10px;
}

.status-badge {
  font-size: 0.7em;
  padding: 3px 6px;
  border-radius: 4px;
  font-weight: bold;
  color: white;
  text-transform: uppercase;
  white-space: nowrap;
}
.status-badge.DONE {
  background-color: #27ae60;
}
.status-badge.WIP {
  background-color: #f39c12;
}
.status-badge.FIX {
  background-color: #c0392b;
}
.status-badge.FEATURE {
  background-color: #2980b9;
}

.duration-wrapper {
  display: flex;
  align-items: center;
  background: #f3f4f6;
  padding: 2px 6px;
  border-radius: 4px;
}
.edit-duration {
  width: 35px;
  background: transparent;
  border: none;
  text-align: right;
  font-family: inherit;
  font-size: 0.85em;
  color: #666;
  font-weight: bold;
  outline: none;
  -moz-appearance: textfield;
}
.edit-message {
  width: 100%;
  border: 1px solid transparent;
  font-family: inherit;
  font-size: 1em;
  color: #333;
  background: transparent;
  padding: 4px;
  border-radius: 4px;
  outline: none;
  transition: all 0.2s;
}
.edit-message:focus {
  background-color: white;
  border-color: #42b883;
  box-shadow: 0 0 0 2px rgba(66, 184, 131, 0.1);
}
.min-label {
  font-size: 0.7em;
  color: #888;
  margin-left: 2px;
}
@media print {
  .edit-message {
    border: none !important;
    resize: none;
  }
  .edit-duration {
    border: none !important;
  }
}
</style>
