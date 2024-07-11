<template>
  <div>
    <form enctype="multipart/form-data" @submit.prevent="handleSubmit" class="flex flex-col">
      <div v-for="(obj, index) in groupFields" :key="index">
        <div class="field-wrapper flex">
          <label :for="'full-name-' + index">{{ obj.fields[0].fieldName }}: </label>
          <div class="flex fields">
            <input @input="onInvalidName" @invalid="onInvalidName" required minlength="6" class="name-field" v-model="obj.fields[0].value" type="text" :id="'full-name-' + index" :placeholder="obj.fields[0].fieldName" />
          </div>
        </div>
        <div class="field-wrapper flex">
          <label :for="'email-' + index">{{ obj.fields[1].fieldName }}: </label>
          <input required @invalid="onInvalidEmail" @input="onInvalidEmail" v-model="obj.fields[1].value" type="email" :id="'email-' + index" :placeholder="obj.fields[1].fieldName" />
        </div>
        <div class="field-wrapper flex">
          <label :for="'mobile-number-' + index">{{ obj.fields[2].fieldName }}</label>
          <input required @invalid="onInvalidMob" maxlength="14" @input="handleMobInput" v-model="obj.fields[2].value" type="text" :id="'mobile-number-' + index" :placeholder="obj.fields[2].fieldName" />
        </div>
        <button @click="removeGroupField(obj)" type="button" class="fit-content">Remove Fields</button>
      </div>

        <div>
        
        <p class="error-p" v-show="!isTwoGroup">Minimum two group fields are required to submit the form</p>
      <button @click="addGroupField" type="button" class="fit-content">Add More Fields</button>
        </div>

      <div class="field-wrapper flex">
        <label :for="'dob-' + id.value">{{ dob.fieldName }}</label>
        <input required @change="formatDate" :max="today" type="date" :id="'dob-' + id.value" />
      </div>
      <div class="field-wrapper flex">
        <label :for="'gender-' + id.value">{{ gender.fieldName }}</label>
        <div>
          <input v-model="gender.value" type="radio" :id="'male-' + id.value" name="gender" value="Male" />
          <label :for="'male-' + id.value">Male</label>
          <input v-model="gender.value" type="radio" :id="'female-' + id.value" name="gender" value="Female" />
          <label :for="'female-' + id.value">Female</label>
          <input v-model="gender.value" type="radio" :id="'others-' + id.value" name="gender" value="Others" />
          <label :for="'others-' + id.value">Others</label>
        </div>
          <p v-show="!isGender && isSubmitted" class="error-p" id="gender-error">Please select your gender</p>
      </div>
      <div class="field-wrapper flex">
        <label :for="'react-' + id.value">{{ languages.fieldName }}</label>
        <div>
          <input class="cb" v-model="languages.value.React" type="checkbox" :id="'react-' + id.value" name="languages" value="React" />
          <label :for="'react-' + id.value">React</label>
          <input class="cb" v-model="languages.value.Vue" type="checkbox" :id="'vue-' + id.value" name="languages" value="Vue" />
          <label :for="'vue-' + id.value">Vue</label>
          <input class="cb" v-model="languages.value.Angular" type="checkbox" :id="'angular-' + id.value" name="languages" value="Angular" />
          <label :for="'angular-' + id.value">Angular</label>
        </div>
          <p v-show="!isCBChecked && isSubmitted" id="language-error" class="error-p">Please select atleast on language</p>
      </div>
      <div class="field-wrapper flex">
        <label :for="'cities-' + id.value">{{ cities.fieldName }}</label>
        <select v-model="cities.value" :id="'cities-' + id.value" name="city" multiple>
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
        <p v-show="!isCities && isSubmitted" class="error-p" id="cities-error">Please select atleast one city</p>
      </div>
      <div class="field-wrapper flex">
        <label >{{ file.fieldName }}</label>
        <input required @change="handleFileChange" type="file" accept=".jpeg, .pdf" />
      </div>
      <input type="submit" value="Submit">
    </form>
  </div>
</template>

<script setup>
  import { reactive, ref, computed } from 'vue';

    let isSubmitted = ref(false)

    let handleFileChange = (event) => {
      const input = event.target.files[0];
      const allowedTypes = ['image/jpeg', 'image/png', 'application/pdf'];
      
      if (!input) {
        event.target.setCustomValidity("Please select a file.");
      } else if (!allowedTypes.includes(input.type)) {
        event.target.setCustomValidity("Invalid file type. Please select a JPEG, PNG, or PDF file.");
      } else {
        event.target.setCustomValidity('');
        file.value = input.name
      }

      // Triggering the invalid event if the file is not valid
      if (event.target.validationMessage) {
        event.target.reportValidity();
      }
    }

    
  let today = new Date().toISOString().split('T')[0];
  let id = ref(1);

  let groupFields = reactive([
    {
      id: id,
      fields: [
        { fieldName: 'Full Name', value: '' },
        { fieldName: 'Email', value: '' },
        { fieldName: 'Mobile Number', value: '' }
      ]
    }, 
    {
      id: id,
      fields: [
        { fieldName: 'Full Name', value: '' },
        { fieldName: 'Email', value: '' },
        { fieldName: 'Mobile Number', value: '' }
      ]
    }
  ]);

    let isTwoGroup = computed(() => groupFields.length >= 2);
    let isCBChecked = computed(() => languages.value.React || languages.value.Vue || languages.value.Angular);
    let isCities = computed(() => cities.value.length !== 0)
    let isGender = computed(() => gender.value !== "")

  const removeGroupField = (obj) => {
    const index = groupFields.findIndex(o => o === obj);
    if (index !== -1) {
      groupFields.splice(index, 1);
    }
  };

  const dob = reactive({ fieldName: 'Date of Birth', value: '' });
  const gender = reactive({ fieldName: 'Gender', value: '' });
  const languages = reactive({ fieldName: 'Languages', value: { React: false, Vue: false, Angular: false } });
  const cities = reactive({ fieldName: 'Cities', value: [] });
  const file = reactive({ fieldName: 'File', value: "" });

  const fieldsList = reactive([dob, gender, languages, cities, file]);

  const emit = defineEmits('form-submitted');

  const handleMobInput = (event) => {
    let currVal = event.target.value.replace(/\D/g, '');
    let formattedVal = '';
    if (currVal.length > 0) {
      formattedVal = '(' + currVal.substring(0, 3);
    }
    if (currVal.length >= 4) {
      formattedVal += ') ' + currVal.substring(3, 6);
    }
    if (currVal.length >= 7) {
      formattedVal += '-' + currVal.substring(6, 10);
    }
    if (currVal.length > 10) {
      formattedVal += ' ' + currVal.substring(10);
    }
    event.target.value = formattedVal;

    onInvalidMob(event)
  };

  const formatDate = (event) => {
    let dateString = event.target.value;
    if (!dateString) return '';

    let options = { year: 'numeric', month: 'long', day: 'numeric' };
    let date = new Date(dateString);

    dob.value = new Intl.DateTimeFormat('en-US', options).format(date);
  };

  const onInvalidName = (event) => {
    const name = event.target
    if(name.value.length === 0){
      name.setCustomValidity('Name cannot be empty')
    }
    else if(name.value.length < 6){
      name.setCustomValidity('Please enter your full name')
    }
    else{
      name.setCustomValidity('')
    }
  }

  const onInvalidEmail = (event) => {
    let email = event.target
    if(email.value.length === 0){
      email.setCustomValidity("Enter your email address")
      return false
    }
    const re = /^(([^<>()[\]\.,;:\s@\"]+(\.[^<>()[\]\.,;:\s@\"]+)*)|(\".+\"))@(([^<>()[\]\.,;:\s@\"]+\.)+[^<>()[\]\.,;:\s@\"]{2,})$/i;
    if(re.test(email.value)){
      email.setCustomValidity("")
    }
    else{
      email.setCustomValidity("Please enter a valid email")
    }
  }

  const onInvalidMob = (event) => {
    let mob = event.target;
    if(mob.value.length === 0){
      mob.setCustomValidity('Enter your mob phone')
    }
    else if(mob.value.length < 14){
      mob.setCustomValidity('Enter a 10 digit number')
    }
    else{
      mob.setCustomValidity('')
    }
  }

const handleSubmit = (event) => {
    isSubmitted.value = true
    if(isTwoGroup.value && isCBChecked.value && isCities && isGender){
        emit('form-submitted', fieldsList, groupFields);
    }
};

  const addGroupField = () => {
    groupFields.push({
      id: id,
      fields: [
        { fieldName: 'Full Name', value: '' },
        { fieldName: 'Email', value: '' },
        { fieldName: 'Mobile Number', value: '' }
      ]
    });
  };
</script>
