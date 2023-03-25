<script>
export default {
    props: ['navigationType', 'currentPage'],
}

</script>

<template>
    <div v-if="navigationType === 'pagination'" class="pagination">
        <button v-on:click="$emit('prev-page', $event)" :disabled="currentPage === 1">Previous</button>
        <span>Page {{ currentPage }}</span>
        <button v-on:click="$emit('next-page', $event)" :disabled="currentPage === totalPages">Next</button>
    </div>
</template>



<style>
h3 {
    text-transform: capitalize;

}

.pagination {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 10px;
    margin: 20px 0;
}

span {
    font-weight: bold;
}

.pokemon-card {
    display: flex;
    flex-direction: column;
    width: 150px;
    padding: 10px;
    border-radius: 5px;
    text-align: center;
    box-shadow: rgba(9, 30, 66, 0.25) 0px 1px 1px, rgba(9, 30, 66, 0.13) 0px 0px 1px 1px;
}
</style>