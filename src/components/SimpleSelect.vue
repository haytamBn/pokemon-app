<script>
export default {
    props: ['label', 'value'],  
}
</script>

<template>
    <div class="container-navigation-type">
        <label for="navigationType">
            {{ label }} :
        </label>
        <select :value="value" id="navigationType" @change="$emit('on-change-select', $event.target.value)">
            <option value="loadMore">Load More</option>
            <option value="pagination">Pagination</option>
        </select>
    </div>
</template>



<style>

label{
    font-weight: bold;
}

.container-navigation-type {
    width: 100%;
    display: flex;
    justify-content: center;
    flex-direction: row;
    align-items: center;
    gap:5px;
}


select {
    align-items: center;
    background-color: white;
    border: 2px solid #111;
    border-radius: 8px;
    box-sizing: border-box;
    color: #111;
    cursor: pointer;
    display: flex;
    font-family: Inter, sans-serif;
    font-size: 16px;
    height: 30px;
    width: 255px;
    justify-content: center;
    line-height: 2px;
    max-width: 100%;
    padding: 0 15px;
    text-align: center;
    text-decoration: none;
    user-select: none;
    -webkit-user-select: none;
    touch-action: manipulation;
}
</style>