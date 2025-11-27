<template>
  <div class="container py-5">
    <div class="experience">
      <h1>{{ pageTitle }}</h1>
      <p>{{ message }}</p>
      
      <section class="contact-section">
        <div class="contact-container">
          <!-- Left side - Contact Information -->
          <div class="contact-info">
            <h2>{{ infoTitle }}</h2>
            <p class="info-description">{{ infoDescription }}</p>
            
            <div class="info-item">
              <div class="icon-container">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                  <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"></path>
                  <polyline points="22,6 12,13 2,6"></polyline>
                </svg>
              </div>
              <div class="info-content">
                <span class="info-label">{{ emailLabel }}</span>
                <span class="info-value">ransaky@gmail.com</span>
              </div>
            </div>
            
            <div class="info-item">
              <div class="icon-container">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                  <path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"></path>
                </svg>
              </div>
              <div class="info-content">
                <span class="info-label">{{ phoneLabel }}</span>
                <span class="info-value">+855 (17) 940 760</span>
              </div>
            </div>
            
            <div class="info-item">
              <div class="icon-container">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                  <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"></path>
                  <circle cx="12" cy="10" r="3"></circle>
                </svg>
              </div>
              <div class="info-content">
                <span class="info-label">{{ locationLabel }}</span>
                <span class="info-value">{{ locationValue }}</span>
              </div>
            </div>
            
            <div class="map-container">
              <iframe 
                src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d15633.264509652054!2d104.8804897!3d11.60079625!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3109522e1adbf683%3A0x3f4395cd35ec9617!2sAEON%20Mall%20Sen%20Sok%20City!5e0!3m2!1sen!2skh!4v1764222712978!5m2!1sen!2skh" 
                width="100%" 
                height="300" 
                style="border:0;" 
                allowfullscreen="" 
                loading="lazy" 
                referrerpolicy="no-referrer-when-downgrade">
              </iframe>
            </div>
          </div>
          
          <!-- Right side - Contact Form -->
          <div class="contact-form">
            <h2>{{ formTitle }}</h2>
            <form @submit.prevent="submitForm">
              <div class="form-group">
                <label for="name">{{ nameLabel }}</label>
                <input 
                  type="text" 
                  id="name" 
                  v-model="formData.name" 
                  required 
                  :placeholder="namePlaceholder"
                >
              </div>
              
              <div class="form-group">
                <label for="email">{{ emailFormLabel }}</label>
                <input 
                  type="email" 
                  id="email" 
                  v-model="formData.email" 
                  required 
                  :placeholder="emailPlaceholder"
                >
              </div>
              
              <div class="form-group">
                <label for="subject">{{ subjectLabel }}</label>
                <input 
                  type="text" 
                  id="subject" 
                  v-model="formData.subject" 
                  required 
                  :placeholder="subjectPlaceholder"
                >
              </div>
              
              <div class="form-group">
                <label for="message">{{ messageLabel }}</label>
                <textarea 
                  id="message" 
                  v-model="formData.message" 
                  rows="5" 
                  required 
                  :placeholder="messagePlaceholder"
                ></textarea>
              </div>
              
              <button type="submit" class="submit-btn" :disabled="isSubmitting">
                <span v-if="!isSubmitting">{{ submitButtonText }}</span>
                <span v-else class="loading">{{ submittingText }}</span>
              </button>
            </form>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<script setup>
import { computed, ref, reactive } from "vue";
import { currentLanguage } from "../stores/languageStore.js";

const message = computed(() => {
  return currentLanguage.value === "KH"
    ? "សូមស្វាគមន៍មកដល់គេហទំព័ររបស់យើងខ្ញុំ"
    : "Welcome to the Contact.";
});

const pageTitle = computed(() => {
  return currentLanguage.value === "KH" ? "ទំព័រទំនាក់ទំនងយើងខ្ញុំ" : "Contact Us";
});

const infoTitle = computed(() => {
  return currentLanguage.value === "KH" ? "ព័ត៌មានយើងខ្ញុំ" : "Information";
});

const infoDescription = computed(() => {
  return currentLanguage.value === "KH" 
    ? "បញ្ហារបស់អ្នក គឺជាបញ្ហារបស់ខ្ញុំ សូមទំនាក់ទំនងមកកាន់យើងខ្ញុំដើម្បីពិភាក្សាស្វែងរកដំណោះស្រាយ" 
    : "I'm always open to discussing new opportunities, creative projects, or just having a chat about technology.";
});

const emailLabel = computed(() => {
  return currentLanguage.value === "KH" ? "អ៊ីម៉េល" : "Email";
});

const phoneLabel = computed(() => {
  return currentLanguage.value === "KH" ? "ទូរស័ព្ទ" : "Phone";
});

const locationLabel = computed(() => {
  return currentLanguage.value === "KH" ? "ទីតាំង" : "Location";
});

const locationValue = computed(() => {
  return currentLanguage.value === "KH" ? "រាជធានីភ្នំពេញ ប្រទេសកម្ពុជា" : "Phnom Penh, Cambodia";
});

const formTitle = computed(() => {
  return currentLanguage.value === "KH" ? "ទំនាក់ទំនងយើងខ្ញុំ" : "Contact Us";
});

const nameLabel = computed(() => {
  return currentLanguage.value === "KH" ? "ឈ្មោះ" : "Name";
});

const namePlaceholder = computed(() => {
  return currentLanguage.value === "KH" ? "បញ្ចូលឈ្មោះរបស់អ្នក" : "Enter your name";
});

const emailFormLabel = computed(() => {
  return currentLanguage.value === "KH" ? "អ៊ីម៉េល" : "Email";
});

const emailPlaceholder = computed(() => {
  return currentLanguage.value === "KH" ? "បញ្ចូលអ៊ីម៉េលរបស់អ្នក" : "Enter your email";
});

const subjectLabel = computed(() => {
  return currentLanguage.value === "KH" ? "ប្រធានបទ" : "Subject";
});

const subjectPlaceholder = computed(() => {
  return currentLanguage.value === "KH" ? "បញ្ចូលប្រធានបទ" : "Enter subject";
});

const messageLabel = computed(() => {
  return currentLanguage.value === "KH" ? "សារ" : "Message";
});

const messagePlaceholder = computed(() => {
  return currentLanguage.value === "KH" ? "បញ្ចូលសាររបស់អ្នក" : "Enter your message";
});

const submitButtonText = computed(() => {
  return currentLanguage.value === "KH" ? "ផ្ញើសារ" : "Send Message";
});

const submittingText = computed(() => {
  return currentLanguage.value === "KH" ? "កំពុងផ្ញើ..." : "Sending...";
});

const isSubmitting = ref(false);

const formData = reactive({
  name: '',
  email: '',
  subject: '',
  message: ''
});

const submitForm = () => {
  isSubmitting.value = true;
  
  // Simulate API call
  setTimeout(() => {
    alert(currentLanguage.value === "KH" 
      ? "សាររបស់អ្នកត្រូវបានផ្ញើដោយជោគជ័យ!" 
      : "Your message has been sent successfully!");
    
    // Reset form
    formData.name = '';
    formData.email = '';
    formData.subject = '';
    formData.message = '';
    isSubmitting.value = false;
  }, 1500);
};
</script>

<style scoped>
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.experience {
  margin-top: 20px;
  animation: fadeIn 0.8s ease-out;
}

.experience h1 {
  font-family: "Khmer OS Muol Light";
  line-height: 80px;
  color: whitesmoke;
  position: relative;
  padding-bottom: 10px;
  text-align: center;
  margin-bottom: 10px;
  font-size: 2.5rem;
  background: linear-gradient(135deg, white, #d1d1d1, #2c3e50);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
}

.experience p {
  font-family: "Khmer OS Battambang";
  text-align: center;
  margin-bottom: 40px;
  font-size: 1.1rem;
  color: #d1d1d1;
  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
}

.contact-section {
  margin-top: 40px;
}

.contact-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 50px;
  align-items: start;
}

.contact-info h2{
  font-family: "Khmer OS Muol Light";
  font-size: 1.8rem;
  margin-bottom: 20px;
  color: whitesmoke;
  position: relative;
  padding-bottom: 10px;
}
.contact-form h2 {
  font-family: "Khmer OS Muol Light";
  font-size: 1.8rem;
  margin-bottom: 20px;
  color: #333;
  position: relative;
  padding-bottom: 10px;
}

.contact-info h2::after,
.contact-form h2::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 60px;
  height: 3px;
  background: linear-gradient(90deg, #4a6cf7, #6a11cb);
  border-radius: 2px;
}

.info-description {
  font-family: "Khmer OS Battambang";
  margin-bottom: 30px;
  line-height: 1.6;
  color: #555;
}

.info-item {
  font-family: "Khmer OS Battambang";
  display: flex;
  align-items: flex-start;
  margin-bottom: 25px;
  padding: 15px;
  border-radius: 8px;
  transition: all 0.3s ease;
  background: #f9f9f9;
}

.info-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
  background: white;
}

.icon-container {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 50px;
  height: 50px;
  background: linear-gradient(135deg, #4a6cf7, #6a11cb);
  border-radius: 50%;
  margin-right: 15px;
  flex-shrink: 0;
}

.icon-container svg {
  color: white;
}

.info-content {
  display: flex;
  flex-direction: column;
}

.info-label {
  
  font-weight: 600;
  margin-bottom: 5px;
  color: #333;
}

.info-value {
  color: #4a6cf7;
  font-weight: 500;
}

.map-container {
  margin-top: 30px;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.map-container:hover {
  transform: scale(1.01);
}

.contact-form {
  background: white;
  padding: 30px;
  border-radius: 10px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  animation: slideInRight 0.8s ease-out;
}

.form-group {
  margin-bottom: 20px;
}

.form-group label {
  font-family: "Khmer OS Battambang";
  font-size: 15px;
  display: block;
  margin-bottom: 8px;
  font-weight: 600;
  color: #333;
}

.form-group input,
.form-group textarea {
   font-family: "Khmer OS Battambang";
  width: 100%;
  padding: 12px 15px;
  border: 1px solid #ddd;
  border-radius: 6px;
  font-size: 1rem;
  transition: all 0.3s ease;
  box-sizing: border-box;
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #4a6cf7;
  box-shadow: 0 0 0 2px rgba(74, 108, 247, 0.2);
}

.submit-btn {
   font-family: "Khmer OS Muol Light";
  width: 100%;
  padding: 14px;
  background: linear-gradient(135deg, #4a6cf7, #6a11cb);
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 1rem;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.submit-btn:hover:not(:disabled) {
  transform: translateY(-3px);
  box-shadow: 0 10px 20px rgba(74, 108, 247, 0.3);
}

.submit-btn:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

.loading {
  display: inline-block;
  animation: pulse 1.5s infinite;
}

/* Animations */
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes slideInRight {
  from {
    opacity: 0;
    transform: translateX(30px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes pulse {
  0% {
    opacity: 1;
  }
  50% {
    opacity: 0.5;
  }
  100% {
    opacity: 1;
  }
}

/* Responsive Design */
@media (max-width: 991px) {
  .experience {
    margin-top: 10%;
  }
  
  .contact-container {
    grid-template-columns: 1fr;
    gap: 40px;
  }
  
  .contact-info {
    animation: slideInLeft 0.8s ease-out;
  }
  
  @keyframes slideInLeft {
    from {
      opacity: 0;
      transform: translateX(-30px);
    }
    to {
      opacity: 1;
      transform: translateX(0);
    }
  }
}

@media (max-width: 768px) {
  .experience h1 {
    font-size: 2rem;
  }
  
  .contact-info h2,
  .contact-form h2 {
    font-size: 1.5rem;
  }
  
  .info-item {
    flex-direction: column;
    align-items: flex-start;
  }
  
  .icon-container {
    margin-bottom: 10px;
  }
  
  .contact-form {
    padding: 20px;
  }
}

@media (max-width: 480px) {
  .container {
    padding: 0 15px;
  }
  
  .experience h1 {
    font-size: 1.8rem;
  }
  
  .experience p {
    font-size: 1rem;
  }
  
  .contact-info h2,
  .contact-form h2 {
    font-size: 1.3rem;
  }
}
</style>