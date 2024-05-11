<template>
  <div class="container">
    <h1>Coffee yang kamu sukai </h1>
    <input type="text" v-model="newTask" placeholder="apa nama cofeenya broo?" class="input-task">
    <button @click="addTask" class="add-button">Tambah</button>
    <table>
      <thead>
        <tr>
          <th>Namanya</th>
          <th>Pengeditan</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>{{ task }}</td>
          <td>
            <button @click="editTask(index)" class="edit-button">Edit</button>
            <button @click="deleteTask(index)" class="delete-button">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
    <div v-if="showEditModal" class="edit-modal">
      <input type="text" v-model="editedTask" placeholder="apa yang mau diedit" class="input-task">
      <button @click="updateTask" class="update-button">Update</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: "",
      tasks: [],
      showEditModal: false,
      editedTask: "",
      editedTaskIndex: null
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== "") {
        this.tasks.push(this.newTask.trim());
        this.newTask = "";
      }
    },
    editTask(index) {
      this.editedTaskIndex = index;
      this.editedTask = this.tasks[index];
      this.showEditModal = true;
    },
    updateTask() {
      if (this.editedTask.trim() !== "") {
        this.tasks[this.editedTaskIndex] = this.editedTask.trim();
        this.editedTask = "";
        this.showEditModal = false;
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    }
  }
};
</script>

<style>
body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  margin: 0;
  padding: 0;
  background-image: url(image/baground.jpg);
  background-size: 100%;
}

.container {
  max-width: 600px;
  margin: 50px auto;
  background-color: #fff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h1 {
  text-align: center;
  margin-bottom: 20px;
  color: #333;
}

.input-task {
  width: calc(70% - 10px); /* Menyesuaikan lebar input dengan margin tombol */
  padding: 10px;
  margin-bottom: 10px;
  border: 2px solid #ced4da;
  border-radius: 4px;
  font-size: 16px;
}

.add-button {
  padding: 10px 20px;
  background-color: #8a3b03;
  color: #fff;
  border: none;
  cursor: pointer;
  border-radius: 4px;
  font-size: 16px;
  margin-left: 10px; /* Menambahkan margin kiri agar terdapat jarak */
}

.add-button:hover {
  background-color: #8a3b03;
}

table {
  width: 100%;
  border-collapse: collapse;
  border: 1px solid #ddd; /* Menambahkan garis pada tabel */
}

thead th {
  background-color: #8a3b03;
  color: #fff;
  padding: 10px;
  text-align: left;
  border-bottom: 2px solid #ddd;
}

tbody td {
  padding: 10px;
  border-bottom: 1px solid #ddd;
}

td {
  border: 1px solid #ddd;
  padding: 8px;

}

.edit-button,
.delete-button {
  padding: 8px 16px;
  margin-left: 10px;
  border: none;
  cursor: pointer;
  border-radius: 4px;
  font-size: 14px;
}

.edit-button {
  background-color: #ffc107;
  color: #333;
}

.edit-button:hover {
  background-color: #e0a800;
}

.delete-button {
  background-color: #dc3545;
  color: #fff;
}

.delete-button:hover {
  background-color: #c82333;
}

.edit-modal {
  margin-top: 20px;
}

.update-button {
  padding: 10px 20px;
  background-color: #28a745;
  color: #fff;
  border: none;
  cursor: pointer;
  border-radius: 4px;
  font-size: 16px;
}

.update-button:hover {
  background-color: #218838;
}
</style>
