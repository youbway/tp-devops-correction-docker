<template>
  <div class="department">
    <a-row type="flex" justify="center">
      <a-col :span="24">
        <h1>Department: {{ name }}</h1>
      </a-col>

      <a-col :span="24">
        <h2>Students:</h2>
      </a-col>

      <a-col :xs="24" :sm="22" :md="12" :lg="8" :xl="5">
        <a-row class="student" v-for="student in students" :key="student.id">
          <a-col :span="24">
            {{ student.firstname }} - {{ student.lastname }}
          </a-col>
        </a-row>
      </a-col>

      <a-col :span="24">
        <a-row type="flex" justify="center">
          <div class="separator" />
        </a-row>
      </a-col>

      <a-col :span="24">
        <a-form layout="inline">
          <a-form-item>
            <a-input placeholder="first name" v-model="firstname" />
          </a-form-item>
          <a-form-item>
            <a-input placeholder="last name" v-model="lastname" />
          </a-form-item>
          <br />
          <a-form-item>
            <a-button @click="addStudent" type="primary">add</a-button>
          </a-form-item>
        </a-form>
      </a-col>
    </a-row>
  </div>
</template>

<script>
import { API_BASE_URL } from "../api";

export default {
  name: "Department",
  data() {
    return {
      firstname: "",
      lastname: "",
      students: [],
      currentDepartment: {}
    };
  },
  computed: {
    name() {
      return this.$route.params.name;
    }
  },
  mounted() {
    this.loadStudents();
    fetch(`${API_BASE_URL}/departments/${this.name}`)
      .then(response => response.json())
      .then(data => {
        this.currentDepartment = data;
      });
  },
  methods: {
    loadStudents() {
      return fetch(`${API_BASE_URL}/departments/${this.name}/students`)
        .then(response => response.json())
        .then(data => {
          this.students = data;
        });
    },
    async addStudent() {
      await fetch(`${API_BASE_URL}/students`, {
        method: "POST",
        headers: {
          Accept: "application/json",
          "Content-Type": "application/json"
        },
        body: JSON.stringify({
          firstname: this.firstname,
          lastname: this.lastname,
          department: {
            id: this.currentDepartment.id,
            name: this.currentDepartment.name
          }
        })
      });
      this.firstname = "";
      this.lastname = "";
      await this.loadStudents();
    }
  }
};
</script>

<style scoped>
.student {
  padding: 8px;
  border-bottom: 1px solid #d9d9d9;
  background: white;
}

.separator {
  width: 70%;
  height: 1px;
  margin: 20px 0;
  background-color: #2323232c;
}
</style>
