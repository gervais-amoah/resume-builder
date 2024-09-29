<script setup>
import { ref } from 'vue'
import ResumeSection from '@/components/ResumeSection.vue'

const personnalInfo = ref({
  name: 'Michaela Scarn',
  title: 'Senior Data Scientist',
  introText:
    'From data cleaning to data analysis to machine learning, I am passionate about everything data.'
})
const imageUrl = ref('/profile_pic.jpg')
const headlines = ref([
  'About me',
  'Contact',
  'Skills',
  'Certifications',
  'Experience',
  'Education'
])
const contact = ref({
  phone: '15713909584',
  email: 'contact@gmail.com',
  address: 'Main St 100, 19777 NY'
})
const highlights = ref([
  'Natural Language Processing with Python (Coursera)',
  'Recommendation Systems with TensorFlow on GCP (Google)'
])
const skills = ref([
  'Python',
  'Pandas',
  'SQL',
  'R',
  'AI',
  'C++',
  'Machine Learning',
  'Hadoop',
  'TensorFlow',
  'PyTorch',
  'NLP'
])
const experience = ref([
  {
    title: 'Senior Data Scientist',
    company: 'ABC Analytics Inc.',
    location: 'London',
    date: '2022 - Present',
    description: [
      'Led a team of data scientists in developing advanced machine learning models for predictive analytics',
      'Designed and implemented a recommendation system that boosted cross-selling, leading to a 20% increase in revenue',
      'Conducted A/B testing and statistical analysis to optimize product features'
    ]
  },
  {
    title: 'Data Scientist',
    company: 'XYZ Data Solutions',
    location: 'London',
    date: '2017 - 2019',
    description: [
      'Developed and deployed machine learning models for fraud detection, reducing fraudulent transactions by 18%',
      'Conducted in-depth exploratory data analysis to identify key trends and insights',
      'Worked on data preprocessing, feature engineering, and model selection to improve model performance'
    ]
  },
  {
    title: 'Data Scientist Trainee',
    company: 'Data Insights Ltd.',
    location: 'New York City',
    date: '2016-2017',
    description: [
      "Collaborated with external partners to integrate third-party data sources, expanding the company's data assets and enhancing predictive modeling capabilities.",
      'Presented data-driven insights and recommendations to executive leadership, influencing strategic decisions and driving revenue growth.'
    ]
  }
])
const education = ref([
  {
    title: 'Master of Science in Data Science',
    university: 'StellarTech University',
    location: 'Starville',
    date: '2020-2022',
    description: [
      'Coursework included advanced machine learning, statistical modeling, and data visualization techniques.',
      "Thesis: 'Predictive Modeling for Customer Churn in E-commerce using Random Forest.'"
    ]
  },
  {
    title: 'Bachelor of Science in Computer Science',
    university: 'Evergreen State University',
    location: 'Springdale',
    date: '2012-2015',
    description: [
      'Relevant coursework in database management, algorithms, and programming languages.',
      "Senior project: 'Development of a Recommender System for Movie Ratings.'"
    ]
  }
])

const updateHeadline = (event, index) => {
  headlines.value[index] = event.target.innerText
}
const updatePersonnalInfo = (event, key) => {
  personnalInfo.value[key] = event.target.innerText
}
const updateContact = (event, index) => {
  contact.value[index] = event.target.innerText
}
const updateSkill = (event, key) => {
  contact.value[key] = event.target.innerText
}
const updateHighlights = (event, key) => {
  highlights.value[key] = event.target.innerText
}

const updateExperience = (event, key, index) => {
  experience.value[index][key] = event.target.innerText
}
const updateExperienceDescription = (event, index1, index2) => {
  experience.value[index1]['description'][index2] = event.target.innerText
}

const updateEducation = (event, key, index) => {
  education.value[index][key] = event.target.innerText
}
const updateEducationDescription = (event, index1, index2) => {
  education.value[index1]['description'][index2] = event.target.innerText
}
</script>

<template>
  <main class="container">
    <div id="resume" class="d-flex">
      <div class="left-col">
        <ResumeSection>
          <img :src="imageUrl" class="profile-pic" alt="profile picture" />

          <h4 class="section-headline" contenteditable @blur="updateHeadline($event, 0)">
            {{ headlines[0] }}
          </h4>
          <span># {{ personnalInfo.name }}</span>
          <div contenteditable @blur="updatePersonnalInfo($event, 'introText')">
            {{ personnalInfo.introText }}
          </div>
        </ResumeSection>

        <ResumeSection>
          <h4 class="section-headline" contenteditable @blur="updateHeadline($event, 1)">
            {{ headlines[1] }}
          </h4>
          <ul>
            <li contenteditable @blur="updateContact($event, 'phone')">{{ contact.phone }}</li>
            <li contenteditable @blur="updateContact($event, 'email')">{{ contact.email }}</li>
            <li contenteditable @blur="updateContact($event, 'address')">{{ contact.address }}</li>
          </ul>
        </ResumeSection>

        <ResumeSection>
          <h4 class="section-headline" contenteditable @blur="updateHeadline($event, 2)">
            {{ headlines[2] }}
          </h4>
          <ul>
            <li
              v-for="(skill, index) in skills"
              :key="index"
              contenteditable
              @blur="updateSkill($event, index)"
            >
              {{ skill }}
            </li>
          </ul>
        </ResumeSection>

        <ResumeSection>
          <h4 class="section-headline" contenteditable @blur="updateHeadline($event, 3)">
            {{ headlines[3] }}
          </h4>
          <ul>
            <li
              v-for="(hlItem, index) in highlights"
              :key="index"
              contenteditable
              @blur="updateHighlights($event, index)"
            >
              {{ hlItem }}
            </li>
          </ul>
        </ResumeSection>
      </div>

      <div class="right-col">
        <div
          class="personal-name"
          :spellcheck="false"
          contenteditable
          @blur="updatePersonnalInfo($event, 'name')"
        >
          {{ personnalInfo.name }}
        </div>
        <div class="personal-title" contenteditable @blur="updatePersonnalInfo($event, 'title')">
          {{ personnalInfo.title }}
        </div>

        <div class="resume-section">
          <h4 class="section-headline" contenteditable @blur="updateHeadline($event, 4)">
            {{ headlines[4] }}
          </h4>
          <div v-for="(exp, index) in experience" :key="index" class="inner-section">
            <div contenteditable="true" @blur="updateExperience($event, 'title', index)">
              {{ exp.title }}
            </div>
            <div class="d-flex justify-content-between">
              <div>
                <span contenteditable="true" @blur="updateExperience($event, 'company', index)">{{
                  exp.company
                }}</span
                >,
                <span contenteditable="true" @blur="updateExperience($event, 'location', index)">{{
                  exp.location
                }}</span>
              </div>
              <div contenteditable="true" @blur="updateExperience($event, 'date', index)">
                {{ exp.date }}
              </div>
            </div>
            <ul>
              <li
                v-for="(desc, innerIndex) in exp.description"
                :key="innerIndex"
                contenteditable="true"
                @blur="updateExperienceDescription($event, index, innerIndex)"
              >
                {{ desc }}
              </li>
            </ul>
          </div>
        </div>

        <div class="resume-section">
          <h4 class="section-headline" contenteditable @blur="updateHeadline($event, 5)">
            {{ headlines[5] }}
          </h4>

          <div v-for="(item, index) in education" :key="index" class="inner-section">
            <div contenteditable="true" @blur="updateEducation($event, 'title', index)">
              {{ item.title }}
            </div>
            <div class="d-flex justify-content-between">
              <div>
                <span contenteditable="true" @blur="updateEducation($event, 'university', index)">
                  {{ item.university }} </span
                >,
                <span contenteditable="true" @blur="updateEducation($event, 'location', index)">
                  {{ item.location }}
                </span>
              </div>

              <div contenteditable="true" @blur="updateEducation($event, 'date', index)">
                {{ item.date }}
              </div>
            </div>
            <ul>
              <li
                v-for="(desc, innerIndex) in item.description"
                :key="innerIndex"
                contenteditable="true"
                @blur="updateEducationDescription($event, index, innerIndex)"
              >
                {{ desc }}
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
#resume {
  box-shadow:
    rgba(50, 50, 93, 0.25) 0px 13px 27px -5px,
    rgba(0, 0, 0, 0.3) 0px 8px 16px -8px;
  /* DIN A4 standard paper size. commonly used for resumes
  For North America letter size use width: 8.5in; height: 11in; */
  height: 297mm;
  width: 210mm;
}

.left-col {
  background-color: var(--background-color-left);
  color: var(--text-color-left);
  border-right: 1px solid var(--highlight-color-left);
  width: 30%;
  padding: 30px;
}

.right-col {
  background-color: var(--background-color-right);
  color: var(--text-color-right);
  width: 70%;
  padding: 30px;
}

.section-headline {
  font-size: 20px;
  font-weight: var(--headline-weight);
  margin-bottom: 15px;
  margin-top: 0;
}

.right-col .section-headline {
  color: var(--highlight-color-right);
}

.left-col .section-headline {
  border-bottom: 1px solid var(--highlight-color-left);
  padding-bottom: 5px;
  margin-right: -30px;
  padding-right: 10px;
  color: var(--highlight-color-left);
}

.personal-name {
  font-weight: 300;
  color: var(--highlight-color-right);
  font-size: 28px;
  border-bottom: 1px solid var(--highlight-color-right);
  margin: 0;
  margin-left: -30px;
  padding-left: 30px;
  padding-bottom: 15px;
}

.personal-title {
  border-bottom: 1px solid var(--highlight-color-right);
  margin: 0 0 20px -30px;
  padding: 15px 0 15px 30px;
  font-weight: 300;
  font-size: 20px;
}

#resume ul {
  padding-inline-start: 16px;
  margin-block-end: 0px;
  margin-block-start: 5px;
}

.profile-pic {
  display: block;
  width: 160px;
  height: 160px;
  border: 5px solid var(--highlight-color-left);
  margin-bottom: 20px;
  object-fit: cover;
  margin-left: auto;
  margin-right: auto;
  border-radius: 50%;
}

.inner-section {
  margin-bottom: 20px;
}
</style>
