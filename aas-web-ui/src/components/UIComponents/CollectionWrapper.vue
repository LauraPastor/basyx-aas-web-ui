<template>
    <v-container fluid class="pa-0">
        <v-expansion-panels multiple class="pa-3">
            <v-expansion-panel v-for="SubmodelElement in SubmodelElementObject.children" :key="SubmodelElement.id">
                <v-expansion-panel-title class="pl-0 py-0">
                    <IdentificationElement
                        :identification-object="SubmodelElement"
                        :model-type="SubmodelElement.modelType"
                        :id-type="'Identification (ID)'"
                        :name-type="'idShort'"></IdentificationElement>
                </v-expansion-panel-title>
                <v-expansion-panel-text>
                    <!-- Display NameplateElement directly when it is no SubmodelElementCollection -->
                    <SubmodelElementWrapper
                        v-if="SubmodelElement.modelType != 'SubmodelElementCollection'"
                        :SubmodelElementObject="SubmodelElement"
                        @update-value="updateCollectionValue"></SubmodelElementWrapper>
                    <!-- Display NameplateElement as SubmodelElementCollection when it is a SubmodelElementCollection -->
                    <CollectionWrapper
                        v-else
                        :SubmodelElementObject="SubmodelElement"
                        @update-value="updateCollectionValue"></CollectionWrapper>
                </v-expansion-panel-text>
            </v-expansion-panel>
        </v-expansion-panels>
    </v-container>
</template>

<script lang="ts">
    import { defineComponent } from 'vue';
    import IdentificationElement from './IdentificationElement.vue';
    import SubmodelElementWrapper from './SubmodelElementWrapper.vue';
    // import CollectionWrapper from './CollectionWrapper.vue';

    export default defineComponent({
        name: 'CollectionWrapper',
        components: {
            // UI Components
            IdentificationElement,
            SubmodelElementWrapper,
        },
        props: ['SubmodelElementObject'],

        data() {
            return {};
        },

        computed: {},

        watch: {},

        mounted() {},

        methods: {
            // Function to update the value of a property
            updateCollectionValue(submodelElement: any) {
                this.$emit('updateValue', submodelElement);
            },
        },
    });
</script>
