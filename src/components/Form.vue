<template>
    <form @submit.prevent="handleSubmit" class="flex flex-col">
        <div class="field-wrapper flex">
            <label>Full Name: </label>
            <div class="flex fields">
                <input v-model="fname" type="text" placeholder="First Name"/>
                <input v-model="lname" type="text" placeholder="Last Name"/>
            </div>
        </div>
        <div class="field-wrapper flex">
            <label>Email: </label>
            <input v-model="email" type="email" placeholder="Email"/>
        </div>
        <div class="field-wrapper flex">
            <label>Mobile Number</label>
            <input v-model="mob_num" type="text" placeholder="Mobile Number"/>
        </div>
        <div class="field-wrapper flex">
            <Label>Date of Birth</Label>
            <input v-model="dob" type="date" />
        </div>
        <div class="field-wrapper flex">
            <label>Gender</label>
            <div>
                <input type="radio" name="gender" value="Male"/>
                <label>Male</label>
                <input type="radio" name="gender" value="Female"/>
                <label>Female</label>
                <input type="radio" name="gender" value="Others"/>
                <label>Others</label>
            </div>
        </div>
        <div class="field-wrapper flex">
            <label>Language</label>
            <div>
                <input type="checkbox" name="gender" value="React"/>
                <label>React</label>
                <input type="checkbox" name="gender" value="Vue"/>
                <label>Vue</label>
                <input type="checkbox" name="gender" value="Angular"/>
                <label>Angular</label>
            </div>
        </div>
        <div class="field-wrapper flex">
            <label>City</label>
            <select name="city" multiple>
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
            <input type="file" accept=".jpeg, .pdf" />
        </div>
        <input type="submit" value="Submit">
    </form>
</template>

<script setup>
    import {ref} from 'vue';

    let fname = ref('')
    let lname = ref('')
    let email = ref('')
    let dob = ref('')
    let mob_num = ref('')

    let handleSubmit = () => {
        console.log(dob.value)
    }
</script>