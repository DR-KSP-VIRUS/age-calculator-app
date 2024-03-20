<template>
    <div class="result">
        <p><span v-if="dataList.years>=0">{{ dataList.years }}</span>
            <span v-else>--</span>
            Years
        </p>
        <p><span v-if="dataList.months>=0">{{ dataList.months }}</span>
            <span v-else>--</span>
            Months
        </p>
        <p><span v-if="dataList.days>=0">{{ dataList.days }}</span>
            <span v-else>--</span>
            Days
        </p>
    </div>
</template>

<script setup>
    const props = defineProps({
        dataList:{
            type:Object,
            required:true,
        },
    });

    console.log(props.dataList)
</script>