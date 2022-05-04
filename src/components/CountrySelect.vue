<script>


export default{
    name:'CountrySelect',
    props:['countries'],
    methods:{
        onChange(){
            const country = this.countries.find(c=>c.ID===this.selected);
            console.log(country);
            this.$emit('get-country',country)
        }
    },
    data(){
        return { 
            selected:0
        }
    }

}

</script>

<template>
   <select v-model="selected" class="form-select  block w-full border p-3 rounded mt-10" @change="onChange" >
       <option value="0">Select Country </option>
       <option  v-for="country in countries"  :value="country.ID">
           {{country.Country}}
       </option>
       

       </select> 
</template>