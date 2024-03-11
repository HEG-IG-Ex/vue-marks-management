<script setup>
import { ref } from 'vue'
import MarksList from '../components/MarksList.vue'
import ListFilters from '../components/ListFilters.vue'

const selectedCourse = ref('all')
const searchQuery = ref('')

const onCourseSelected = (course) => {
  selectedCourse.value = course
}

const onSearchChanged = (query) => {
  searchQuery.value = query
}
</script>

<template>
  <ListFilters @onCourseSelected="onCourseSelected" @onSearchChanged="onSearchChanged" />
  <MarksList :selectedCourse="selectedCourse" :searchQuery="searchQuery" />
</template>
