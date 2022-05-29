<template>
  <div class="chip-container">
    <div class="chip" v-for="(chip, i) of chips" :key="chip.label">
      {{ chip.label }}
      <i @click="deleteChip(i)">X</i>
    </div>
    <input
      type="text"
      @input="showModal"
      v-model="inputSomething"
      @keypress.enter="saveChip"
      @keydown.delete="backspaceDelete"
    />
  </div>
  <div class="modal" v-if="isActive">
    <p v-for="item in users" :key="item.id" @click="saveFromModal(item.label)">
      {{ item.label }}
    </p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isActive: false,
      inputSomething: "",
      chips: [],
      users: [
        { id: 0, label: "Nikola" },
        { id: 1, label: "Milica" },
        { id: 2, label: "Ana" },
        { id: 3, label: "Milos" },
      ],
      count: 0,
    };
  },
  methods: {
    showModal() {
      this.inputSomething !== ""
        ? (this.isActive = true)
        : (this.isActive = false);
    },
    saveChip() {
      this.chips.push({ id: this.count++, label: this.inputSomething });
      this.inputSomething = "";
    },
    deleteChip(index) {
      this.chips.splice(index, 1);
    },
    backspaceDelete() {
      if (this.inputSomething === "") {
        this.chips.splice(this.chips.length - 1);
      }
    },
    saveFromModal(user) {
      this.chips.push({ id: this.count++, label: user });
    },
  },
};
</script>

<style scoped>
.chip-container {
  width: 400px;
  border: 1px solid #ccc;
  min-height: 34px;
  display: flex;
  flex-wrap: wrap;
  align-content: space-between;
  margin: 0 auto;
}
input {
  flex: 1 1 auto;
  width: 30px;
  border: none;
  outline: none;
  padding: 4px;
}
.chip {
  margin: 4px;
  background: #e0e0e0;
  padding: 0px 4px;
  border: 1px solid #ccc;
  border-radius: 3px;
  display: flex;
  align-items: center;
}
i {
  cursor: pointer;
  opacity: 0.56;
  margin-left: 8px;
}
.modal {
  border: 1px solid red;
  width: 200px;
  margin: 0 auto;
}
</style>
