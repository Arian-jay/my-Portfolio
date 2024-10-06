<template>
  <v-app>
    <v-app-bar app color="rgba(18, 18, 18, 0.9)" elevation="1" class="px-4">
      <v-app-bar-title class="text-primary font-weight-bold">AJP</v-app-bar-title>
      <v-spacer></v-spacer>
      <v-btn
        v-for="item in menuItems"
        :key="item.title"
        :href="item.href"
        text
        class="hidden-sm-and-down"
        @click.prevent="scrollTo(item.href)"
        :color="item.color"
      >
        {{ item.title }}
      </v-btn>
      <v-app-bar-nav-icon @click="drawer = !drawer" class="hidden-md-and-up"></v-app-bar-nav-icon>
    </v-app-bar>

    <v-navigation-drawer v-model="drawer" temporary class="bg-grey-darken-3">
      <v-list>
        <v-list-item
          v-for="item in menuItems"
          :key="item.title"
          :href="item.href"
          @click="scrollTo(item.href); drawer = false"
        >
          <v-list-item-title>{{ item.title }}</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-main>
      <v-container fluid class="pa-0">
        <section id="home" class="py-16 hero-section">
          <v-row align="center" justify="center" class="text-center">
            <v-col cols="12">
              <v-avatar size="200" class="mb-4">
                <v-img src="../assets/profile.jpg" alt="Arian Jay Prisco"></v-img>
              </v-avatar>
              <h1 class="text-h2 font-weight-bold mb-2 animated fadeIn text-shadow">Arian Jay Prisco</h1>
              <p class="text-h5 text-grey-lighten-1 mb-6 animated fadeIn delay-1 text-shadow">Full-Stack Developer & UI/UX Enthusiast</p>
              <v-btn color="primary" size="x-large" href="#projects" @click.prevent="scrollTo('#projects')" class="animated fadeInUp delay-2">
                View My Work
                <v-icon right>mdi-arrow-right</v-icon>
              </v-btn>
            </v-col>
          </v-row>
        </section>

        <section id="about" class="py-16 about-section">
          <v-container>
            <h2 class="text-h3 font-weight-bold mb-8 text-center animated fadeIn section-title">About Me</h2>
            <v-row justify="center">
              <v-col cols="12" md="8">
                <v-card class="bg-glass animated fadeInUp">
                  <v-card-text class="text-body-1">
                    <p class="mb-4">
                      I'm a passionate full-stack developer with a keen eye for design and user experience. With expertise in Vue.js, React, Node.js, and various backend technologies, I specialize in creating responsive and user-friendly web applications that not only look great but also perform exceptionally well.
                    </p>
                    <p class="mb-4">
                      My journey in web development started 5 years ago, and since then, I've had the opportunity to work on diverse projects ranging from e-commerce platforms to complex data visualization tools. I'm always excited to take on new challenges and learn cutting-edge technologies to stay ahead in this ever-evolving field.
                    </p>
                    <p>
                      When I'm not coding, you'll find me exploring the great outdoors, experimenting with new recipes in the kitchen, or contributing to open-source projects. I believe in the power of community and continuous learning, which is why I regularly attend tech meetups and conferences.
                    </p>
                  </v-card-text>
                </v-card>
              </v-col>
            </v-row>
          </v-container>
        </section>

        <section id="skills" class="py-16 skills-section">
          <v-container>
            <h2 class="text-h3 font-weight-bold mb-8 text-center animated fadeIn section-title">Skills & Expertise</h2>
            <v-row justify="center">
              <v-col cols="12" md="8">
                <v-card class="bg-glass animated fadeInUp">
                  <v-card-text>
                    <v-row>
                      <v-col v-for="skill in skills" :key="skill.name" cols="12" sm="6" md="4">
                        <v-card class="skill-card" flat>
                          <v-card-text class="text-center">
                            <v-icon size="48" :color="skill.color" class="mb-2">{{ skill.icon }}</v-icon>
                            <h3 class="text-h6 mb-2">{{ skill.name }}</h3>
                            <v-progress-circular
                              :rotate="360"
                              :size="100"
                              :width="15"
                              :model-value="skill.level"
                              :color="skill.color"
                            >
                              {{ skill.level }}%
                            </v-progress-circular>
                          </v-card-text>
                        </v-card>
                      </v-col>
                    </v-row>
                  </v-card-text>
                </v-card>
              </v-col>
            </v-row>
          </v-container>
        </section>

        <section id="projects" class="py-16 projects-section">
          <v-container>
            <h2 class="text-h3 font-weight-bold mb-8 text-center animated fadeIn section-title">My Projects</h2>
            <v-row>
              <v-col v-for="(project, index) in projects" :key="project.title" cols="12" md="4">
                <v-card class="project-card h-100 animated fadeInUp " :style="{ animationDelay: `${index * 0.2}s` }">
                  <v-img :src='project.image' height="200" cover class="project-image">
                    <template v-slot:placeholder>
                      <v-row class="fill-height ma-0" align="center" justify="center">
                        <v-progress-circular indeterminate color="primary"></v-progress-circular>
                      </v-row>
                    </template>
                  </v-img>
                  <v-card-title class="text-h5 text-white section-title">{{ project.title }}</v-card-title>
                  <v-card-text>
                    <p class="mb-4 text-grey-lighten-1">{{ project.description }}</p>
                    <v-chip-group>
                      <v-chip v-for="tech in project.technologies" :key="tech" class="text" small>
                        {{ tech }}
                      </v-chip>
                    </v-chip-group>
                  </v-card-text>
                  <v-card-actions>
                    <v-btn color="primary" variant="outlined" :href="project.link" target="_blank">
                      View Project
                      <v-icon right>mdi-open-in-new</v-icon>
                    </v-btn>
                    <v-btn color="primary" variant="outlined" :href="project.github" target="_blank">
                      <v-icon left>mdi-github</v-icon>
                      GitHub
                    </v-btn>
                  </v-card-actions>
                </v-card>
              </v-col>
            </v-row>
          </v-container>
        </section>

        <section id="education" class="py-16 education-section">
          <v-container>
            <h2 class="text-h3 font-weight-bold mb-8 text-center animated fadeIn section-title">Education</h2>
            <v-row justify="center">
              <v-col cols="12" md="8">
                <v-card class="bg-glass animated fadeInUp">
                  <v-card-title class="text-h5">Bachelor of Science in Information Technology</v-card-title>
                  <v-card-subtitle class="text-h6">Caraga State University</v-card-subtitle>
                  <v-card-text>
                    <p class="mb-2">Graduated with honors, specializing in Web Technologies and Artificial Intelligence</p>
                    <p class="text-grey">2022 - 2026</p>
                  </v-card-text>
                  <v-card-actions>
                    <v-chip color="primary" small>Dean's List</v-chip>
                    <v-chip color="primary" small class="ml-2">Research Assistant</v-chip>
                  </v-card-actions>
                </v-card>
              </v-col>
            </v-row>
          </v-container>
        </section>

        <section id="contact" class="py-16 contact-section">
          <v-container>
            <h2 class="text-h3 font-weight-bold mb-8 text-center animated fadeIn section-title">Get In Touch</h2>
            <v-row justify="center">
              <v-col cols="12" md="8">
                <v-card class="bg-glass animated fadeInUp">
                  <v-card-text>
                    <v-form @submit.prevent="submitForm">
                      <v-text-field
                        v-model="form.name"
                        label="Name"
                        required
                        prepend-icon="mdi-account"
                        variant="outlined"
                      ></v-text-field>
                      <v-text-field
                        v-model="form.email"
                        label="Email"
                        type="email"
                        required
                        prepend-icon="mdi-email"
                        variant="outlined"
                      ></v-text-field>
                      <v-textarea
                        v-model="form.message"
                        label="Message"
                        required
                        prepend-icon="mdi-message-text"
                        variant="outlined"
                      ></v-textarea>
                      <v-btn type="submit" color="primary" block class="mt-4" size="large">
                        Send Message
                        <v-icon right>mdi-send</v-icon>
                      </v-btn>
                    </v-form>
                  </v-card-text>
                </v-card>
              </v-col>
            </v-row>
          </v-container>
        </section>
      </v-container>
    </v-main>

    <v-footer class="bg-grey-darken-4 py-4">
      <v-container>
        <v-row align="center" justify="space-between">
          <v-col cols="12" md="6" class="text-center text-md-left">
            <span class="text-grey">© 2024 Arian Jay Prisco. All rights reserved.</span>
          </v-col>
          <v-col cols="12" md="6" class="text-center text-md-right">
            <v-btn v-for="link in socialLinks" :key="link.icon" :href="link.url" icon target="_blank" class="mx-2 social-icon">
              <v-icon>{{ link.icon }}</v-icon>
            </v-btn>
          </v-col>
        </v-row>
      </v-container>
    </v-footer>
  </v-app>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import todoListImage from '../assets/todoList.jpg'
import weatherImage from '../assets/weather.png'
import portfolioImage from '../assets/portfolio.jpg'


const drawer = ref(false)

const menuItems = [
  { title: 'Home', href: '#home' , color: '#ffffff'},
  { title: 'About', href: '#about', color: '#ffffff'},
  { title: 'Skills', href: '#skills', color: '#ffffff'},
  { title: 'Projects', href: '#projects', color: '#ffffff'},
  { title: 'Education', href: '#education', color: '#ffffff'},
  { title: 'Contact', href: '#contact', color: '#ffffff'},
]

const skills = [
  { name: 'Vue.js', level: 90, icon: 'mdi-vuejs', color: '#41B883' },
  { name: 'React', level: 85, icon: 'mdi-react', color: '#61DAFB' },
  { name: 'Node.js', level: 80, icon: 'mdi-nodejs', color: '#339933' },
  { name: 'JavaScript', level: 95, icon: 'mdi-language-javascript', color: '#F7DF1E' },
  { name: 'HTML/CSS', level: 100, icon: 'mdi-language-html5', color: '#E34F26' },
  { name: 'Python', level: 75, icon: 'mdi-language-python', color: '#3776AB' },
]

const projects = [
  {
    title: 'To-do List Web App', color: 'white',
    description: 'A simple, user-friendly to-do list app with task management, local storage for persistence, and dark mode support. It allows users to add, edit, delete, and mark tasks as completed. The design is responsive and optimized for both mobile and desktop.',
    image: todoListImage,
    link: 'https://todolist-prisco.vercel.app/',
    github: 'https://github.com/Arian-jay/todolist',
    technologies: ['Vue.js', 'Local Storage', 'CSS3'],
  },
  {
    title: 'Portfolio Website', color: 'white',
    description: 'A personal portfolio website built with Bootstrap, showcasing my skills, projects, and experience. The website is fully responsive, ensuring smooth navigation on both desktop and mobile devices. It includes sections like About Me, Skills, Projects, and Contact.',
    image: portfolioImage,
    link: 'https://arian-jay.github.io/Bootstrap_prisco/',
    github: 'https://github.com/Arian-jay/Bootstrap_prisco',
    technologies: ['HTML5', 'CSS3', 'Bootstrap', 'JavaScript'],
  },
  {
    title: 'Weather Track App', color: 'white',
    description: 'A web application that provides real-time weather updates for any location. Users can search for cities or use their current location to get detailed weather information, including temperature, humidity. The app features a clean, user-friendly interface with dynamic weather icons.',
    image: weatherImage,
    link: 'https://weather-tracker-prisco.vercel.app/',
    github: 'https://github.com/Arian-jay/weather_app',
    technologies: ['Vue.js', 'OpenWeatherMap API', 'Axios'],
  },
]

const socialLinks = [
  { icon: 'mdi-github', url: 'https://github.com/Arian-jay' },
  { icon: 'mdi-facebook', url: 'https://web.facebook.com/profile.php?id=100009416138022' },
  { icon: 'mdi-instagram', url: 'https://www.instagram.com/ari_ariannnn' },
  { icon: 'mdi-email', url: 'mailto:priscoarianjay159@gmail.com' },
]

const form = ref({
  name: '',
  email: '',
  message: '',
})

const submitForm = () => {
  console.log('Form submitted:', form.value)
  form.value = { name: '', email: '', message: '' }
}

const scrollTo = (elementId) => {
  const element = document.querySelector(elementId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth', block: 'start' })
  }
}

// Smooth scroll animation
const animateOnScroll = () => {
  const elements = document.querySelectorAll('.animated')
  elements.forEach((element) => {
    const elementTop = element.getBoundingClientRect().top
    const elementBottom = element.getBoundingClientRect().bottom
    if (elementTop < window.innerHeight && elementBottom > 0) {
      element.classList.add('fadeIn')
    }
  })
}

onMounted(() => {
  window.addEventListener('scroll', animateOnScroll)
  animateOnScroll() // Initial check
})

onUnmounted(() => {
  window.removeEventListener('scroll', animateOnScroll)
})
</script>

<style scoped>
.v-application {
  background-color: #121212 !important;
}

.hero-section {
  background-image: linear-gradient(rgba(0, 0, 0, 0.7), rgba(0, 0, 0, 0.7)), url('../assets/hero-bg.jpg');
  background-size: cover;
  background-position: center;
  color: white;
  min-height: 100vh;
  display: flex;
  align-items: center;
}

.nav {
  color: #ffffff;
}

p {
  color: #ffffff;
  font-size: 1.1rem;
  line-height: 1.6;
}

h2 {
  color: #ffffff;
}

.about-section,
.skills-section,
.projects-section,
.education-section,
.contact-section {
  background-color: rgba(18, 18, 18, 0.95);
}

.text-primary {
  color: #4CAF50 !important;
}

.bg-primary {
  background-color: #4CAF50 !important;
}

.v-btn.v-btn--icon {
  color: #4CAF50;
}

.v-progress-circular {
  margin: 1rem;
}

.v-card {
  transition: all 0.5s ease;
  background-color: rgba(255, 255, 255, 0.05) !important;
}

.v-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.4);
}

.v-chip {
  margin-right: 8px;
  margin-bottom: 8px;
}

.skill-card {
  background-color: rgba(255, 255, 255, 0.05) !important;
  border-radius: 8px;
  transition: all 0.5s ease;
}

.skill-card:hover {
  background-color: rgba(255, 255, 255, 0.1) !important;
  transform: translateY(-5px);
}

.project-card {
  overflow: hidden;
}

.project-image {
  transition: transform 0.5s ease;
}

.project-card:hover .project-image {
  transform: scale(1.05);
}

.social-icon {
  transition: all 0.3s ease;
}

.social-icon:hover {
  transform: translateY(-3px);
  color: #4CAF50 !important;
}

.bg-glass {
  background-color: rgba(255, 255, 255, 0.1) !important;
  backdrop-filter: blur(10px);
  border-radius: 10px;
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.text-shadow {
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
}

.section-title {
  position: relative;
  display: inline-block;
  padding-bottom: 10px;
}

.section-title::after {
  content: '';
  position: absolute;
  left: 50%;
  bottom: 0;
  transform: translateX(-50%);
  width: 50px;
  height: 3px;
  background-color: #4CAF50;
}

.section-title-proj::after {
  content: '';
  position: absolute;
  left: 50%;
  bottom: 0;
  transform: translateX(-50%);
  width: 50px;
  height: 3px;
  background-color: #4CAF50;
}

/* Animations */
.animated {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.8s ease, transform 0.8s ease;
}

.fadeIn {
  opacity: 1;
  transform: translateY(0);
}

.delay-1 {
  transition-delay: 0.2s;
}

.delay-2 {
  transition-delay: 0.4s;
}
.text{
  color:rgba(206, 255, 8, 0.4)
}
</style>