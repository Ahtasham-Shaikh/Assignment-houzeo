<template>
  <div>
    <form enctype="multipart/form-data" @submit.prevent="handleSubmit" class="flex flex-col">
      <div v-for="(obj, index) in groupFields" :key="index">
        <div class="field-wrapper flex">
          <label :for="'full-name-' + index">{{ obj.fields[0].fieldName }}: </label>
          <div class="flex fields">
            <input v-model="obj.fields[0].value" type="text" :id="'full-name-' + index" :placeholder="obj.fields[0].fieldName" />
          </div>
        </div>
        <div class="field-wrapper flex">
          <label :for="'email-' + index">{{ obj.fields[1].fieldName }}: </label>
          <input v-model="obj.fields[1].value" type="email" :id="'email-' + index" :placeholder="obj.fields[1].fieldName" />
        </div>
        <div class="field-wrapper flex">
          <label :for="'mobile-number-' + index">{{ obj.fields[2].fieldName }}</label>
          <input maxlength="14" @input="handleMobInput(obj.fields[2])" v-model="obj.fields[2].value" type="text" :id="'mobile-number-' + index" :placeholder="obj.fields[2].fieldName" />
        </div>
        <button @click="removeGroupField(obj)" type="button" class="fit-content">Remove Fields</button>
      </div>

      <button @click="addGroupField" type="button" class="fit-content">Add More Fields</button>

      <div class="field-wrapper flex">
        <label :for="'dob-' + id.value">{{ dob.fieldName }}</label>
        <input @change="formatDate" :max="today" v-model="dob.value" type="date" :id="'dob-' + id.value" />
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
      </div>
      <div class="field-wrapper flex">
        <label :for="'react-' + id.value">{{ languages.fieldName }}</label>
        <div>
          <input v-model="languages.value.React" type="checkbox" :id="'react-' + id.value" name="languages" value="React" />
          <label :for="'react-' + id.value">React</label>
          <input v-model="languages.value.Vue" type="checkbox" :id="'vue-' + id.value" name="languages" value="Vue" />
          <label :for="'vue-' + id.value">Vue</label>
          <input v-model="languages.value.Angular" type="checkbox" :id="'angular-' + id.value" name="languages" value="Angular" />
          <label :for="'angular-' + id.value">Angular</label>
        </div>
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
      </div>
      <div class="field-wrapper flex">
        <label >{{ file.fieldName }}</label>
        <input @change="handleFileChange" type="file" accept=".jpeg, .pdf" />
      </div>
      <input type="submit" value="Submit">
    </form>
  </div>
</template>

<script setup>
  import { reactive, ref } from 'vue';
  import FilesInput from './FilesInput.vue';

    let handleFileChange = (event) => {
        let fileName = event.target.files[0].name
        file.value = fileName
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
    }
  ]);

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

  const handleMobInput = (field) => {
    let currVal = field.value.replace(/\D/g, '');
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
    field.value = formattedVal;
  };

  const formatDate = (event) => {
    let dateString = event.target.value;
    if (!dateString) return '';

    let options = { year: 'numeric', month: 'long', day: 'numeric' };
    let date = new Date(dateString);

    dob.value = new Intl.DateTimeFormat('en-US', options).format(date);
  };

  const handleSubmit = () => {
    emit('form-submitted', fieldsList, groupFields);
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
