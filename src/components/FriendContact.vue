<template>
    <li>
        <h2>{{ name }} {{ friendIsFavorite === '1' ? '(Favorite)' : '' }} </h2>
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
            type: String,
            required: false,
            default: '0',
            validator: function(value) {
                return value === '1' || value === '0';
            }
        },

    },
    data() {
        return {
            detailsAreVisible: false,
            friendIsFavorite: this.isFavorite
        }
    },
    methods: {
        toggleDetails() {
            this.detailsAreVisible = !this.detailsAreVisible;
        },
        toggleFavorite() {
            if (this.friendIsFavorite === "1") {
                this.friendIsFavorite = "0";
            } else {
                this.friendIsFavorite = "1";
            }
        }
    },
    computed: {
        isDetailVisible() {
            return this.detailsAreVisible ? 'Hide' : 'Show';
        }
    }
};
</script>