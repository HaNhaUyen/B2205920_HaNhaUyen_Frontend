<template>
  <div class="page">
    <h4>Thêm Liên hệ</h4>
    <ContactForm
      :contact="contact"
      @submit:contact="addContact"
      @delete:contact="deleteContact"
    />
  </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
  components: { ContactForm },
  data() {
    return {
      contact: {
        name: "",
        email: "",
        address: "",
        phone: "",
        favorite: false,
      },
    };
  },
  methods: {
    async addContact(data) {
      try {
        await ContactService.create(data);
        alert("Đã thêm liên hệ thành công!");
        this.$router.push({ name: "contactbook" });
      } catch (error) {
        console.error(error);
        alert("Lỗi khi thêm liên hệ.");
      }
    },
    async deleteContact() {
      if (confirm("Bạn muốn xóa liên hệ này")) {
        try {
          await ContactService.delete(this.contact._id);
          this.$router.push({ name: "contactbook" });
        } catch (error) {
          console.log(error);
        }
      }
    },
  },
};
</script>

<style scoped>
.page {
  max-width: 400px;
  margin: 20px auto;
  padding: 15px;
  border: 1px solid #ccc;
  border-radius: 8px;
}
h4 {
  text-align: center;
  margin-bottom: 20px;
}
</style>
