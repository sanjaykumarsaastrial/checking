<script setup>
import { ref, reactive, computed, watch } from 'vue'

const student = reactive({
  name: '',
  age: '',
  city: ''
})

const students = ref([])

const showSuccess = ref(false)
const showStudents = ref(true)

function addStudent() {
  if (
    student.name &&
    student.age &&
    student.city
  ) {
    students.value.push({
      name: student.name,
      age: student.age,
      city: student.city
    })

    showSuccess.value = true

    student.name = ''
    student.age = ''
    student.city = ''
  }
}

function toggleStudents() {
  showStudents.value = !showStudents.value
}

const totalStudents = computed(() => {
  return students.value.length
})

watch(
  () => students.value.length,
  () => {
    console.log('Student Count Changed')
  }
)
</script>

<template>
  <h1>Student Management</h1>

  <input
    v-model="student.name"
    placeholder="Enter Name"
  >

  <br><br>

  <input
    v-model="student.age"
    placeholder="Enter Age"
  >

  <br><br>

  <input
    v-model="student.city"
    placeholder="Enter City"
  >

  <br><br>

  <button @click="addStudent">
    Add Student
  </button>

  <h3 v-if="showSuccess">
    Student Added Successfully
  </h3>

  <h2>
    Total Students : {{ totalStudents }}
  </h2>

  <button @click="toggleStudents">
    {{ showStudents ? 'Hide Students' : 'Show Students' }}
  </button>

  <div v-show="showStudents">

    <div
      v-for="(stu,index) in students"
      :key="index"
      style="border:1px solid black;
             padding:10px;
             margin:10px;"
    >
      <h3>Name : {{ stu.name }}</h3>

      <h3>Age : {{ stu.age }}</h3>

      <h3>City : {{ stu.city }}</h3>

      <p
        :style="{
          color: stu.age >= 18
          ? 'green'
          : 'red'
        }"
      >
        {{ stu.age >= 18
          ? 'Eligible'
          : 'Not Eligible'
        }}
      </p>

    </div>

  </div>

</template>