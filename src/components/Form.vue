<template>
    <form enctype='multipart/form-data' @submit.prevent="handleSubmit" class="flex flex-col">
        <div class="field-wrapper flex">
            <label>Full Name: </label>
            <div class="flex fields">
                <input v-model="fname.value" type="text" placeholder="First Name"/>
                <input v-model="lname.value" type="text" placeholder="Last Name"/>
            </div>
        </div>
        <div class="field-wrapper flex">
            <label>Email: </label>
            <input v-model="email.value" type="email" placeholder="Email"/>
        </div>
        <div class="field-wrapper flex">
            <label>Mobile Number</label>
            <input v-model="mob_num.value" type="text" placeholder="Mobile Number"/>
        </div>
        <div class="field-wrapper flex">
            <label>Date of Birth</label>
            <input v-model="dob.value" type="date" />
        </div>
        <div class="field-wrapper flex">
            <label>Gender</label>
            <div>
                <input v-model="gender.value" type="radio" name="gender" value="Male"/>
                <label>Male</label>
                <input v-model="gender.value" type="radio" name="gender" value="Female"/>
                <label>Female</label>
                <input v-model="gender.value" type="radio" name="gender" value="Others"/>
                <label>Others</label>
            </div>
        </div>
        <div class="field-wrapper flex">
            <label>Language</label>
            <div>
                <input v-model="languages.value" type="checkbox" name="gender" value="React"/>
                <label>React</label>
                <input v-model="languages.value" type="checkbox" name="gender" value="Vue"/>
                <label>Vue</label>
                <input v-model="languages.value" type="checkbox" name="gender" value="Angular"/>
                <label>Angular</label>
            </div>
        </div>
        <div class="field-wrapper flex">
            <label>City</label>
            <select v-model="cities.value" name="city" multiple>
                <option value="mumbai">Mumbai</option>
                <option value="delhi">Delhi</option>
                <option value="london">London</option>
                <option value="singapore">Singapore</option>
                <option value="dubai">Dubai</option>
                <option value="moscow">Moscow</option>
                <option value="jaipur">Jaipur</option>
                <option value="chennai">Chennai</option>
                <option value="los angeles">Los Angeles</option>
            </select>
        </div>
        <div class="field-wrapper flex">
            <label>File</label>
            <FilesInput :file-model="files.value" ></FilesInput>
        </div>
        <input type="submit" value="Submit">
    </form>
</template>

<script setup>
    import FilesInput from './FilesInput.vue'
    import {reactive} from 'vue';

    let createReactive = (str, initVal) => {
        return reactive({
            fieldName: str,
            value: initVal
        })
    }

    let fname = createReactive('First Name', '')
    let lname = createReactive('Last Name', '')
    let email = createReactive('Email', '')
    let dob = createReactive('dob', '')
    let mob_num = createReactive('Mobile Number', '')
    let gender = createReactive('Gender', '')
    let languages = createReactive('Languages', [])
    let cities = createReactive('Cities', [])
    let files = createReactive('Files', [])

    let fieldsList = [fname, lname, email, dob, mob_num, gender, languages, cities, files]

    let emit = defineEmits('form-submitted')

    let handleSubmit = () => {
        emit('form-submitted', fieldsList)
        console.log(files.value)
    }
</script>