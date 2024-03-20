<template>
  <div class="calculator">
    <AddForm @addData="handleSubmit"/>
    <DataList :dataList="data" />
  </div>
</template>

<script setup>
  import { ref } from 'vue';
  import './assets/main.css'
  import AddForm from './components/AddForm.vue';
  import DataList from './components/DataList.vue';

  const data = ref({
    day:'',
    month:'',
    year:''
  });

  const handleSubmit = (submittedData) => { 
    data.value = submittedData;
  }
</script>