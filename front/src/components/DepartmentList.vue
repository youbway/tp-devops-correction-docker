<template>
  <div class="department-list">
    <h1>Departments</h1>
    <a-row type="flex" justify="center">
      <a-col :xs="24" :sm="22" :md="12" :lg="8" :xl="5">
        <a-row
          class="department"
          v-for="department in departments"
          :key="department.id"
        >
          <router-link :to="`/departments/${department.name}`">
            <a-col :span="12">{{ department.id }}</a-col>
            <a-col :span="12">{{ department.name }}</a-col>
          </router-link>
        </a-row>
      </a-col>
    </a-row>
  </div>
</template>

<script>
import { API_BASE_URL } from "../api";

export default {
  name: "DepartmentList",
  data() {
    return {
      departments: []
    };
  },
  mounted() {
    fetch(`${API_BASE_URL}/departments`)
      .then(response => response.json())
      .then(data => {
        this.departments = data;
      });
  }
};
</script>

<style scoped>
.department {
  padding: 12px;
  border-bottom: 1px solid #d9d9d9;
  background: white;
}

.department:hover {
  background-color: #face53;
}

a,
a:hover {
  color: #232323;
}
</style>
