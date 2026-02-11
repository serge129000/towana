<template>
  <div class="landing-page">
    <!-- Navigation -->
    <nav class="navbar">
      <div class="nav-container">
        <div class="logo-nav">Towiana's</div>
        <button @click="openContactModal" class="contact-btn-nav">Contact Us</button>
      </div>
    </nav>

    <!-- Hero Section -->
    <section class="hero">
      <div class="hero-content">
        <div class="logo-main">
          <h1 class="logo-title">Towiana's</h1>
          <h2 class="logo-subtitle">MOBILE NOTARY <span class="ampersand">&</span> BUSINESS SERVICES</h2>
        </div>
        <p class="hero-description">
          Professional notary services at your doorstep. Reliable, fast, and available throughout Alabama.
        </p>
        <button @click="openContactModal" class="cta-button">
          Book a Service
          <span class="arrow">→</span>
        </button>
      </div>
      <div class="hero-image">
        <div class="notary-illustration">
          <div class="stamp-circle"></div>
        </div>
      </div>
    </section>

    <!-- Services Section -->
    <section class="services" id="services">
      <div class="container">
        <h2 class="section-title">Our Services</h2>
        <div class="services-grid">
          <div class="service-card" v-for="service in services" :key="service.title">
            <div class="service-icon">{{ service.icon }}</div>
            <h3>{{ service.title }}</h3>
            <p>{{ service.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- About Section -->
    <section class="about">
      <div class="container">
        <div class="about-content">
          <h2 class="section-title">Why Choose Us?</h2>
          <div class="features-grid">
            <div class="feature">
              <div class="feature-icon">🚗</div>
              <h3>Mobile Service</h3>
              <p>We come to you, wherever you are in Alabama</p>
            </div>
            <div class="feature">
              <div class="feature-icon">⚡</div>
              <h3>Fast & Reliable</h3>
              <p>Professional and efficient service every time</p>
            </div>
            <div class="feature">
              <div class="feature-icon">✓</div>
              <h3>Certified</h3>
              <p>Licensed notary with years of experience</p>
            </div>
            <div class="feature">
              <div class="feature-icon">📱</div>
              <h3>Available</h3>
              <p>Flexible hours to fit your schedule</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Coverage Section -->
    <section class="coverage">
      <div class="container">
        <h2 class="section-title">Coverage Area</h2>
        <div class="coverage-info">
          <div class="coverage-icon">📍</div>
          <h3>Serving Alabama State at Large</h3>
          <p>We serve the entire state of Alabama with the same level of professionalism</p>
        </div>
      </div>
    </section>

    <!-- Contact Modal -->
    <Transition name="modal">
      <div v-if="showModal" class="modal-overlay" @click="closeContactModal">
        <div class="modal-content" @click.stop>
          <button class="close-btn" @click="closeContactModal">&times;</button>
          <h3 class="modal-title">Book Your Service</h3>
          
          <form @submit.prevent="handleSubmit" class="booking-form">
            <div class="form-row">
              <div class="form-group">
                <label for="firstName">First Name</label>
                <input 
                  type="text" 
                  id="firstName" 
                  v-model="formData.firstName" 
                  required
                  placeholder="Your first name"
                />
              </div>
              
              <div class="form-group">
                <label for="lastName">Last Name</label>
                <input 
                  type="text" 
                  id="lastName" 
                  v-model="formData.lastName" 
                  required
                  placeholder="Your last name"
                />
              </div>
            </div>

            <div class="form-row">
              <div class="form-group">
                <label for="phone">Phone</label>
                <input 
                  type="tel" 
                  id="phone" 
                  v-model="formData.phone" 
                  required
                  placeholder="(555) 123-4567"
                />
              </div>
              
              <div class="form-group">
                <label for="email">Email</label>
                <input 
                  type="email" 
                  id="email" 
                  v-model="formData.email" 
                  required
                  placeholder="your@email.com"
                />
              </div>
            </div>

            <div class="form-group">
              <label for="documentType">Document Type</label>
              <select id="documentType" v-model="formData.documentType" required>
                <option value="">Select a type</option>
                <option value="gnw">GNW</option>
                <option value="bill-of-sale">Bill of Sale</option>
                <option value="poa">Power of Attorney (PoA)</option>
                <option value="marriage-cert">Marriage Certificate</option>
                <option value="other">Other</option>
              </select>
            </div>

            <div class="form-group">
              <label class="checkbox-label">
                <input 
                  type="checkbox" 
                  v-model="formData.needsMobileService"
                />
                <span>I need mobile service</span>
              </label>
            </div>

            <div class="form-group">
              <label for="additionalServices">Additional Services</label>
              <textarea 
                id="additionalServices" 
                v-model="formData.additionalServices"
                rows="4"
                placeholder="Describe your additional needs..."
              ></textarea>
            </div>

            <button type="submit" class="submit-btn">
              Submit Request
            </button>
          </form>
        </div>
      </div>
    </Transition>

    <!-- Footer -->
    <footer class="footer">
      <div class="container">
        <div class="footer-content">
          <div class="footer-logo">
            <h3>Towiana's</h3>
            <p>Mobile Notary & Business Services</p>
          </div>
          <div class="footer-contact">
            <p>📧 www.tmnbs.com</p>
            <p>📍 Alabama State at Large</p>
          </div>
        </div>
        <div class="footer-bottom">
          <p>&copy; 2026 Towiana's Mobile Notary & Business Services. All rights reserved.</p>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue'

const showModal = ref(false)

const services = [
  {
    icon: '📄',
    title: 'GNW',
    description: 'General notarization services for all your official documents'
  },
  {
    icon: '📋',
    title: 'Bill of Sale',
    description: 'Notarization of sales contracts for vehicles and other property'
  },
  {
    icon: '⚖️',
    title: 'Power of Attorney',
    description: 'Notarized powers of attorney for your legal representations'
  },
  {
    icon: '💍',
    title: 'Marriage Certificate',
    description: 'Certification of marriage documents and other civil records'
  }
]

const formData = reactive({
  firstName: '',
  lastName: '',
  phone: '',
  email: '',
  documentType: '',
  needsMobileService: false,
  additionalServices: ''
})

const openContactModal = () => {
  showModal.value = true
  document.body.style.overflow = 'hidden'
}

const closeContactModal = () => {
  showModal.value = false
  document.body.style.overflow = 'auto'
}

const handleSubmit = () => {
  console.log('Form submitted:', formData)
  alert('Thank you! Your request has been submitted successfully. We will contact you soon.')
  closeContactModal()
  // Reset form
  Object.assign(formData, {
    firstName: '',
    lastName: '',
    phone: '',
    email: '',
    documentType: '',
    needsMobileService: false,
    additionalServices: ''
  })
}
</script>

<style scoped>
.landing-page {
  min-height: 100vh;
  background: #ffffff;
}

/* Navigation */
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  background: rgba(255, 255, 255, 0.98);
  backdrop-filter: blur(10px);
  box-shadow: 0 2px 20px rgba(0, 0, 0, 0.05);
  z-index: 100;
  padding: 1rem 0;
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo-nav {
  font-size: 1.5rem;
  font-weight: 700;
  background: linear-gradient(135deg, #e91e63 0%, #9c27b0 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-family: 'Brush Script MT', cursive;
}

.contact-btn-nav {
  background: linear-gradient(135deg, #e91e63 0%, #9c27b0 100%);
  color: white;
  border: none;
  padding: 0.75rem 1.5rem;
  border-radius: 25px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.contact-btn-nav:hover {
  transform: translateY(-2px);
  box-shadow: 0 5px 20px rgba(156, 39, 176, 0.3);
}

/* Hero Section */
.hero {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem;
  max-width: 1200px;
  margin: 0 auto;
  padding: 8rem 2rem 2rem;
  align-items: center;
  min-height: 75vh;
}

.hero-content {
  animation: fadeInUp 0.8s ease;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.logo-main {
  margin-bottom: 2rem;
}

.logo-title {
  font-size: 4rem;
  font-weight: 700;
  background: linear-gradient(135deg, #e91e63 0%, #9c27b0 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-family: 'Brush Script MT', cursive;
  margin-bottom: 0.5rem;
  line-height: 1.2;
}

.logo-subtitle {
  font-size: 1.2rem;
  font-weight: 600;
  color: #333;
  letter-spacing: 3px;
}

.ampersand {
  color: #e91e63;
  font-size: 1.5rem;
}

.hero-description {
  font-size: 1.25rem;
  color: #666;
  line-height: 1.8;
  margin-bottom: 2rem;
}

.cta-button {
  background: linear-gradient(135deg, #e91e63 0%, #9c27b0 100%);
  color: white;
  border: none;
  padding: 1.25rem 2.5rem;
  font-size: 1.1rem;
  font-weight: 600;
  border-radius: 50px;
  cursor: pointer;
  transition: all 0.3s ease;
  display: inline-flex;
  align-items: center;
  gap: 0.75rem;
  box-shadow: 0 10px 30px rgba(156, 39, 176, 0.3);
}

.cta-button:hover {
  transform: translateY(-3px);
  box-shadow: 0 15px 40px rgba(156, 39, 176, 0.4);
}

.arrow {
  transition: transform 0.3s ease;
}

.cta-button:hover .arrow {
  transform: translateX(5px);
}

.hero-image {
  display: flex;
  justify-content: center;
  align-items: center;
}

.notary-illustration {
  width: 400px;
  height: 400px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  animation: float 3s ease-in-out infinite;
  box-shadow: 0 20px 60px rgba(118, 75, 162, 0.3);
}

@keyframes float {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-20px);
  }
}

.stamp-circle {
  width: 250px;
  height: 250px;
  border: 15px dashed rgba(255, 255, 255, 0.4);
  border-radius: 50%;
}

/* Services Section */
.services {
  background: #f8f9fa;
  padding: 5rem 2rem;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
}

.section-title {
  font-size: 2.5rem;
  text-align: center;
  margin-bottom: 3rem;
  color: #333;
  font-weight: 700;
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
}

.service-card {
  background: white;
  padding: 2.5rem;
  border-radius: 20px;
  text-align: center;
  transition: all 0.3s ease;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.05);
}

.service-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.1);
}

.service-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.service-card h3 {
  font-size: 1.5rem;
  color: #333;
  margin-bottom: 1rem;
  font-weight: 600;
}

.service-card p {
  color: #666;
  line-height: 1.6;
}

/* About Section */
.about {
  padding: 5rem 2rem;
  background: white;
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  margin-top: 3rem;
}

.feature {
  text-align: center;
  padding: 2rem;
}

.feature-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.feature h3 {
  font-size: 1.3rem;
  color: #333;
  margin-bottom: 0.75rem;
  font-weight: 600;
}

.feature p {
  color: #666;
  line-height: 1.6;
}

/* Coverage Section */
.coverage {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  padding: 5rem 2rem;
  color: white;
}

.coverage .section-title {
  color: white;
}

.coverage-info {
  text-align: center;
  max-width: 600px;
  margin: 0 auto;
}

.coverage-icon {
  font-size: 4rem;
  margin-bottom: 1.5rem;
}

.coverage-info h3 {
  font-size: 2rem;
  margin-bottom: 1rem;
  font-weight: 600;
}

.coverage-info p {
  font-size: 1.2rem;
  opacity: 0.95;
  line-height: 1.6;
}

/* Modal */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  padding: 2rem;
}

.modal-content {
  background: white;
  padding: 2.5rem;
  border-radius: 20px;
  max-width: 600px;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
  position: relative;
  animation: slideUp 0.3s ease;
}

@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(50px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.close-btn {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: none;
  border: none;
  font-size: 2rem;
  cursor: pointer;
  color: #999;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  transition: all 0.3s ease;
}

.close-btn:hover {
  background: #f5f5f5;
  color: #333;
}

.modal-title {
  text-align: center;
  font-size: 2rem;
  color: #333;
  margin-bottom: 2rem;
  font-weight: 600;
}

.booking-form {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.form-group label {
  font-weight: 600;
  color: #555;
  font-size: 0.95rem;
}

.form-group input,
.form-group select,
.form-group textarea {
  padding: 0.875rem 1rem;
  border: 2px solid #e0e0e0;
  border-radius: 10px;
  font-size: 1rem;
  transition: all 0.3s ease;
  font-family: inherit;
}

.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #9c27b0;
  box-shadow: 0 0 0 3px rgba(156, 39, 176, 0.1);
}

.checkbox-label {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  cursor: pointer;
  font-weight: 500;
  color: #555;
}

.checkbox-label input[type="checkbox"] {
  width: 20px;
  height: 20px;
  cursor: pointer;
  accent-color: #9c27b0;
}

.submit-btn {
  background: linear-gradient(135deg, #e91e63 0%, #9c27b0 100%);
  color: white;
  border: none;
  padding: 1rem 2rem;
  font-size: 1.1rem;
  font-weight: 600;
  border-radius: 10px;
  cursor: pointer;
  transition: all 0.3s ease;
  margin-top: 1rem;
  box-shadow: 0 4px 15px rgba(156, 39, 176, 0.3);
}

.submit-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(156, 39, 176, 0.4);
}

/* Modal Transitions */
.modal-enter-active,
.modal-leave-active {
  transition: opacity 0.3s ease;
}

.modal-enter-from,
.modal-leave-to {
  opacity: 0;
}

/* Footer */
.footer {
  background: #1a1a1a;
  color: white;
  padding: 3rem 2rem 1.5rem;
}

.footer-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
  max-width: 1200px;
  margin: 0 auto 2rem;
}

.footer-logo h3 {
  font-size: 1.8rem;
  margin-bottom: 0.5rem;
  font-family: 'Brush Script MT', cursive;
  background: linear-gradient(135deg, #e91e63 0%, #9c27b0 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.footer-logo p {
  color: #999;
  font-size: 0.9rem;
}

.footer-contact p {
  margin-bottom: 0.5rem;
  color: #999;
}

.footer-bottom {
  text-align: center;
  padding-top: 2rem;
  border-top: 1px solid #333;
  color: #666;
  font-size: 0.9rem;
}

/* Responsive */
@media (max-width: 968px) {
  .hero {
    grid-template-columns: 1fr;
    padding-top: 6rem;
    text-align: center;
  }

  .hero-image {
    order: -1;
  }

  .notary-illustration {
    width: 300px;
    height: 300px;
  }

  .stamp-circle {
    width: 180px;
    height: 180px;
  }

  .logo-title {
    font-size: 3rem;
  }

  .footer-content {
    grid-template-columns: 1fr;
    text-align: center;
  }
}

@media (max-width: 640px) {
  .form-row {
    grid-template-columns: 1fr;
  }

  .logo-title {
    font-size: 2.5rem;
  }

  .logo-subtitle {
    font-size: 1rem;
  }

  .section-title {
    font-size: 2rem;
  }

  .modal-content {
    padding: 1.5rem;
  }

  .notary-illustration {
    width: 250px;
    height: 250px;
  }
}
</style>
