<template>
    <li>
        <h2>{{ name }} {{ isFavorite ? '(Favorite)' : '' }} </h2>
        <button @click="toggleFavorite">Favorite</button>
        <button @click="toggleDetails">{{ isDetailVisible }} Details</button>
        <ul v-if="detailsAreVisible">
            <li><strong>Email: {{ emailAddress }}</strong></li>
            <li><strong>Phone: {{ phoneNumber }}</strong></li>
        </ul>
    </li>
</template>

<script>
export default {
    props: {
        id: {
            type: String,
            required: true
        },
        name: {
            type: String,
            required: true,
        },
        phoneNumber: {
            type: String,
            required: true,
        },
        emailAddress: {
            type: String,
            required: true,
        },
        isFavorite: {
            type: Boolean,
            required: false,
            default: false,
        },

    },
    emits: [
        'toggle-favorite'
    ],
    data() {
        return {
            detailsAreVisible: false
        }
    },
    methods: {
        toggleDetails() {
            this.detailsAreVisible = !this.detailsAreVisible;
        },
        toggleFavorite() {
            this.$emit('toggle-favorite', this.id);
        },
    },
    computed: {
        isDetailVisible() {
            return this.detailsAreVisible ? 'Hide' : 'Show';
        }
    }
};
</script>