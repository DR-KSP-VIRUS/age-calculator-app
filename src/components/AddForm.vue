<template>
    <form class="calculator-form" @submit.prevent="onAddData">
        <div :class="!error.day ? 'form-group':'form-group error-text' ">
            <label for="day">Day</label>
            <input type="text" name="day" id="day" 
                :class="validateDate ? 'form-control':!error.day?'form-control error':'form-control' " 
                placeholder="DD"
                v-model="day"
            />
            <span class="error-text">{{ error.day }}</span>
        </div>
        <div :class="!error.month ? 'form-group':'form-group error-text' ">
            <label for="month">Month</label>
            <input type="text" name="month" id="month" 
            :class="validMonth ? 'form-control':'form-control error' " 
                placeholder="MM"
                v-model="month"
            />
            <span class="error-text">{{ error.month }}</span>
        </div>
        <div :class="!error.year ? 'form-group':'form-group error-text' ">
            <label for="year">Year</label>
            <input type="text" name="year" id="year" 
                :class="validYear ? 'form-control':'form-control error' " 
                placeholder="YYYY"
                v-model="year"
            />
            <span class="error-text">{{ error.year }}</span>
        </div>
        <button type="submit" class="btn-float">
            <img :src="iconArrow" alt="icon">
        </button>
    </form>

</template>


<script setup>
    import { ref, computed } from 'vue';
    import moment from 'moment';
    import iconArrow from '../assets/images/icon-arrow.svg';


    const day = ref('');
    const month = ref('');
    const year = ref('');

    const error = ref({
        day:'',
        month:'',
        year:''
    })

    const emit = defineEmits(['addData'])

    const validateDate = computed(() => {
        if (day.value && !(moment(`${day.value}-${month.value}-${year.value}`,'DD-MM-YYYY').isValid() && day.value < 32)){
            error.value.day = "Day must be valid"
            return false
        }else{
            error.value.day = ""
            return true;
        }
    });
    const validMonth = computed(() => {
        if (month.value && !(month.value < 13)){
            error.value.month = "Month must be valid";
            return false
        }else{
            error.value.month = "";
            return true
        }
    });
    const validYear = computed(() => {
        if (year.value && !(+year.value <= new Date().getFullYear())){
            error.value.year = 'Year must be in the past';
            return false
        }else{
            error.value.year = '';
            return true
        }
    });

    const onAddData = () => {
        if ((!day.value || !validateDate.value) || (!month.value || !validMonth.value) || (!year.value || !validYear.value) ) {
            error.value.day = 'require field is empty';
            error.value.month = 'require field is empty';
            error.value.year = 'require field is empty'
            return
        }
        let prevDate = + new Date(+year.value,+month.value,+day.value);
        const formData = {
            years : Math.floor(moment().diff(moment(`${year.value}${month.value}${day.value}`,'YYYYMMDD'),'years',true)),
            months : Math.floor(prevDate % 365 / 30),
            days : Math.floor(prevDate % 365 % 30),
        }

        emit('addData',formData);
    }
    
</script>