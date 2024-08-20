<!-- eslint-disable prettier/prettier -->
<template>
  <div class="container">
    <header>
      <img
        src="@/assets/energeek2.png"
        alt="Logo"
        class="logo"
        style="height: 60px; margin-top: 131px; margin-bottom: 50px" />
    </header>

    <div class="form-container">
      <div class="input-group">
        <label for="name">Nama</label>
        <input v-model="form.name" type="text" id="name" placeholder="Nama" />
      </div>
      <div class="input-group">
        <label for="username">Username</label>
        <input
          v-model="form.username"
          type="text"
          id="username"
          placeholder="Username" />
      </div>
      <div class="input-group">
        <label for="email">Email</label>
        <input
          v-model="form.email"
          type="email"
          id="email"
          placeholder="Email" />
      </div>
    </div>

    <div class="todo-list-header">
      <h2 style="font-weight: 500">To Do List</h2>
      <button @click="addTask" class="add-todo-btn">+ Tambah To Do</button>
    </div>

    <div class="todo-list">
      <div v-for="(task, index) in form.tasks" :key="index" class="task-group">
        <div class="input-group task-title">
          <label :for="'task_description_' + index">Judul To Do</label>
          <input
            v-model="task.description"
            :id="'task_description_' + index"
            placeholder="Contoh: Perbaikan api master" />
        </div>
        <div class="input-group task-category">
          <label :for="'task_category_' + index">Kategori</label>
          <select v-model="task.category_id" :id="'task_category_' + index">
            <option
              v-for="category in categories"
              :key="category.id"
              :value="category.id">
              {{ category.name }}
            </option>
          </select>
        </div>
        <button @click="removeTask(index)" class="delete-btn">🗑️</button>
      </div>
    </div>

    <button @click="submitForm" class="submit-btn">SIMPAN</button>
  </div>
</template>

<script>
import axios from "axios";
import Swal from "sweetalert2";

export default {
  data() {
    return {
      categories: [],
      form: {
        name: "",
        username: "",
        email: "",
        tasks: [{ description: "", category_id: "" }],
      },
    };
  },
  methods: {
    async fetchCategories() {
      try {
        const response = await axios.get(
          "http://127.0.0.1:8000/api/categories"
        );
        this.categories = response.data;
      } catch (error) {
        console.error("Error fetching categories:", error);
        Swal.fire({
          icon: "error",
          title: "Oops...",
          text: "Failed to fetch categories!",
        });
      }
    },
    validateEmail(email) {
      // Regex untuk memeriksa format email yang valid
      const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      return re.test(String(email).toLowerCase());
    },
    addTask() {
      this.form.tasks.push({ description: "", category_id: "" });
    },
    removeTask(index) {
      this.form.tasks.splice(index, 1);
    },
    async submitForm() {
      if (!this.validateEmail(this.form.email)) {
        Swal.fire({
          icon: "error",
          title: "Oops...",
          text: "Email tidak valid!",
        });
        return; // Berhenti jika email tidak valid
      }

      try {
        const response = await axios.post(
          "http://127.0.0.1:8000/api/tasks",
          this.form
        );
        Swal.fire({
          icon: "success",
          title: "Success!",
          text: "Task sukses dibuat!",
        });
      } catch (error) {
        console.error("There was an error creating the task:", error);
        Swal.fire({
          icon: "error",
          title: "Oops...",
          text: "User sudah ada!",
        });
      }
    },
  },

  mounted() {
    this.fetchCategories();
  },
};
</script>
<style scoped>
.container {
  max-width: 800px;
  margin: auto;
  padding: 20px;
}

.logo {
  display: block;
  margin: 0 auto 20px;
}

.form-container {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}

.input-group {
  flex: 1;
  margin-right: 10px;
}

.input-group:last-child {
  margin-right: 0;
}

label {
  display: block;
  margin-bottom: 5px;
}

input,
select {
  width: 100%;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ddd;
}

.todo-list-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
}

.todo-list {
  margin-bottom: 20px;
}

.task-group {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.task-title {
  flex: 3;
  margin-right: 10px;
}

.task-category {
  flex: 1;
  margin-right: 10px;
}

.delete-btn {
  background-color: #f44336;
  border: none;
  color: white;
  padding: 10px;
  border-radius: 10px;
  cursor: pointer;
  align-self: flex-end;
  height: 42px;
}

.add-todo-btn {
  background-color: #ffe2e5;
  color: #f1416c;
  border: none;
  padding: 10px;
  border-radius: 5px;
  cursor: pointer;
  margin-top: 10px;
}

.submit-btn {
  background-color: #4caf50;
  color: white;
  border: none;
  padding: 15px;
  border-radius: 5px;
  width: 100%;
  cursor: pointer;
  font-size: 18px;
}
</style>
