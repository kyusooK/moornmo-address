<template>

    <div>
        <div class="detail-title">
        Weather
        </div>
        <v-col>
            <Number label="Degree" v-model="value.degree" :editMode="editMode"/>
            <Number label="Precipitation" v-model="value.precipitation" :editMode="editMode"/>
            <Number label="Humidity" v-model="value.humidity" :editMode="editMode"/>
            <Number label="Wind" v-model="value.wind" :editMode="editMode"/>
        </v-col>

        <v-card-actions v-if="inList">
            <slot name="actions"></slot>
        </v-card-actions>
    </div>
</template>

<script>
import BaseEntity from './base-ui/BaseEntity'

export default {
    name: 'Weather',
    mixins:[BaseEntity],
    components:{
    },
    data: () => ({
        path: '',
    }),
    props: {
    },
    watch: {
        value(val){
            this.value = val;
            this.change();
        },
    },
    async created(){
        if (this.value && this.value.id !== undefined) {
            this.value = await this.repository.findById(this.value.id)
        }
    },
    methods: {
        pick(val){
            this.value = val;
            this.change();
        },
    }
}
</script>

