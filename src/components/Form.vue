<template>
  <form @submit.prevent="handleSubmit">
      <div class="form-control control-input">
          <input type="text" placeholder="Enter place" v-model="area">
      </div>
      <div class="form-control control-search">
          <input type="submit" value="Search">
      </div>
  </form>
</template>

<script>
import { ref } from '@vue/reactivity'
export default {
    name: 'Form',
    emits: ['onSubmit'],
    setup(props, { emit }){
        let area = ref('');
        const handleSubmit = () => {
            emit('onSubmit', area.value);
            area.value = '';
        };
        return { area, handleSubmit };
    }

}
</script>

<style>
    form{
        display: grid;
        gap: 10px;
    }
    form .form-control{
        width: 100%;
    }
    form .control-input{
        border: 1px solid #ccc;
    }
    form input{
        width: 100%;
        border: none;
        padding: 8px;
    }
    form input[type="text"]:focus{
        outline: 1px solid rgb(18, 196, 18);
    }
    form input[type="submit"]{
        background: rgb(18, 196, 18);
        color: #ccc;
        font-weight: bold;
        letter-spacing: 1px;
        cursor: pointer;
    }
    form input[type="submit"]:hover{
        background: rgb(6, 175, 6);
    }
</style>