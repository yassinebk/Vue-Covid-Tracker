<script  lang="ts">
import hourglassGIF from "@/assets/hourglass.gif";
import DataTitle from "@/components/DataTitle.vue";
import DataBoxes from '@/components/DataBoxes.vue';
import CountrySelect from "@/components/CountrySelect.vue"

export default { 
    name:"Home",
    components:{
        DataTitle,
        DataBoxes,
        CountrySelect
    },
    data(){
        return {
            loading:true,
            title:'Global',
            dataDate:"",
            stats:{},
            countries:[],
            loadingImage:hourglassGIF
        }
    },
    methods:{ 
        async onClick(){
                    this.loading=true;
                    const data = await this.fetchCovidData();
                    this.title="Global",
                    this.stats=data.Global;
                    this.loading=false;
        },
        async fetchCovidData(){
            const res = await fetch("https://api.covid19api.com/summary");
            return res.json();
        },
        async getCountry(country :any ){

                console.log(country);
                this.stats = country; 
                this.title= country.Country;
                // const res = await 
        }

    },
    async created(){
        const data = await this.fetchCovidData();
        console.log(data);
        this.dataDate=data.Date;
        this.stats=data.Global;
        this.countries= data.Countries;
        this.loading=false;
        
        
    }
}

</script>

<template>
<main v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate"></DataTitle>
    <DataBoxes :stats="stats"/>
    <CountrySelect :countries="countries" @get-country="getCountry"/>
    <button @click="onClick" v-if="stats.Country" class="bg-blue-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-blue-500">
        Clear Country 
    </button>
    
</main>

<main v-else class="flex flex-col items-center align-center justify-center mx-auto ">
    <div class="text-gray-500 text-3xl mt-10 mb-6">
        Fetching Data
    </div>
    <img :src="loadingImage" alt="Loading Image" class="w-24">
</main>
</template>
