<template>
  <div class="about">
    <user-courses-table />
  </div>
</template>

<script>
import UserCoursesTable from '@/components/UserCoursesTable.vue'

export default {
  name: 'about',
  components: {
    UserCoursesTable
  }
}
</script>
