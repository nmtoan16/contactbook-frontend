<template>
    <div v-if="addContact" class="page">
        <h4>Thêm mới Liên hệ</h4>
        <ContactForm :contact="contact" @submit:contact="addNewContact" />
        <p>{{ message }}</p>
    </div>
</template>
<script>
import ContactForm from "@/components/ContactForm.vue"; import ContactService from "@/services/contact.service";
export default {
    components: {
        ContactForm,
    },
    props: {
        id: "",
    },
    data() {
        return {
            contact: {},
            message: "",
            addContact: true
        };
    },
    methods: {
        async addNewContact(data){
            try {
                await ContactService.create(data);
                this.message = "Liên hệ được tạo thành công.";
                setTimeout(() => {
                    this.addContact = false;
                }, 1000);
                
            } catch (error) {
                console.log(error);
            }
        }
    },
    created() {
        //this.getContact(this.id);
        this.message = "";
    },
};
</script>