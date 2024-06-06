<script setup>
const props = defineProps(['currentPage', 'lastPage'])
const router = useRouter()

console.log('test' + props.lastPage)
const emit = defineEmits(['onPageChange'])

const changePage = (page) => {
  if (page >= 1 && page <= props.lastPage) {
    emit('onPageChange', page);
    router.push({ query: { ...router.currentRoute.value.query, page: page } });
  }
};

</script>

<template>
  <div>
    <button @click="changePage(props.currentPage - 1)" :disabled="props.currentPage === 1">Previous</button>
    <span>Page {{ props.currentPage }} of {{ lastPage }}</span>
    <button @click="changePage(props.currentPage + 1)" :disabled="props.currentPage === props.lastPage">Next</button>
  </div>
</template>
