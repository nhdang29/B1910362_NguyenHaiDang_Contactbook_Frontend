<template>
    <AppHeader class="mb-3"/>
    <div v-if="contact" class="page">
        <h4>Thên Liên hệ</h4>
        <ContactForm 
            :contact="contact" 
            @submit:contact="createContact" 
        />
        <p>{{ message }}</p>
    </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";
import AppHeader from "../components/AppHeader.vue";

export default {
    components: {
        AppHeader,
        ContactForm,
    },
    data() {
        return {
            contact: null,
            message: "",
        };
    },
    methods: {
        async createContact(data) {
            try {
                await ContactService.create(data);
                this.message = "Thêm liên hệ thành công.";
            } catch (error) {
                console.log(error);
            }
        },
    },
    created() {
        this.contact = {};
        this.message = "";
    },
};
</script>   