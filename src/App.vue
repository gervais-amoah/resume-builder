<script setup>
import ContactInfo from '@/components/ContactInfo.vue'
import EditButtons from '@/components/EditButtons.vue'
import ToggleSwitch from '@/components/ToggleSwitch.vue'
import ResumeSection from '@/components/ResumeSection.vue'
import SectionHeadline from '@/components/SectionHeadline.vue'
import SidebarMenu from '@/components/SidebarMenu.vue'
import { computed, ref } from 'vue'
import ColorInput from './components/ColorInput.vue'
import ImgUpload from './components/ImgUpload.vue'
import SelectInput from './components/SelectInput.vue'
import WidthPicker from './components/WidthPicker.vue'
import ExportPdf from './components/ExportPdf.vue'

const colors = ref({
  left: {
    highlight: '#82c0cc',
    text: '#ffffff',
    background: '#3943b7'
  },
  right: {
    highlight: '#3943b7',
    text: '#000505',
    background: '#ffffff'
  }
})

const leftColumnWidth = ref(30)
const leftColumnWidthValue = computed(() => leftColumnWidth.value + '%')
const rightColumnWidthValue = computed(() => 100 - leftColumnWidth.value + '%')

const imageShape = ref('round')
const headlineWeight = ref('400')

const cssVariables = computed(() => {
  return {
    '--highlight-color-left': colors.value.left.highlight,
    '--background-color-left': colors.value.left.background,
    '--text-color-left': colors.value.left.text,
    '--highlight-color-right': colors.value.right.highlight,
    '--background-color-right': colors.value.right.background,
    '--text-color-right': colors.value.right.text,
    '--left-column-width': leftColumnWidthValue.value,
    '--right-column-width': rightColumnWidthValue.value,
    '--headline-weight': headlineWeight.value,
    '--image-shape': imageShape.value
  }
})

const personnalInfo = ref({
  name: 'Michaela Scarn',
  title: 'Senior Data Scientist',
  introText:
    'From data cleaning to data analysis to machine learning, I am passionate about everything data.'
})
const imageUrl = ref('/profile.png')
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

const updateHeadline = (newVal, index) => {
  headlines.value[index] = newVal
}
const updatePersonnalInfo = (event, key) => {
  personnalInfo.value[key] = event.target.innerText
}
const updateContact = (newVal, index) => {
  contact.value[index] = newVal
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

const addExperience = () => {
  experience.value.unshift({
    title: 'Job Title',
    company: 'Company',
    location: 'Location',
    date: 'date range',
    description: ['description']
  })
}
const addEducation = () => {
  education.value.unshift({
    title: 'Education title',
    university: 'University',
    location: 'Location',
    date: 'date range',
    description: ['Summa cum laude, GPA 1.0']
  })
}

const removeExperience = (index) => {
  experience.value.splice(index, 1)
}
const removeEducation = (index) => {
  education.value.splice(index, 1)
}

const editing = ref(true)
const editModeToggled = (isChecked) => {
  editing.value = isChecked
}

const showImage = ref(true)
const toggleImageDisplay = (isChecked) => {
  showImage.value = isChecked
}
</script>

<template>
  <main class="container">
    <SidebarMenu>
      <ToggleSwitch @switch-toogled="editModeToggled" label="Edit mode" off-label="Export Mode" />

      <ExportPdf v-show="!editing" />

      <div v-show="editing">
        <hr />
        <h2>Left column</h2>
        <ColorInput
          label="Highlight color"
          :default-color="colors.left.highlight"
          @color-changed="(event) => (colors.left.highlight = event)"
        />
        <ColorInput
          :default-color="colors.left.text"
          label="Text color"
          @color-changed="(event) => (colors.left.text = event)"
        />
        <ColorInput
          :default-color="colors.left.background"
          label="Background color"
          @color-changed="(event) => (colors.left.background = event)"
        />
      </div>
      <div v-show="editing">
        <hr />
        <h2>Right column</h2>
        <ColorInput
          :default-color="colors.right.highlight"
          label="Highlight color"
          @color-changed="(event) => (colors.right.highlight = event)"
        />
        <ColorInput
          :default-color="colors.right.text"
          label="Text color"
          @color-changed="(event) => (colors.right.text = event)"
        />
        <ColorInput
          :default-color="colors.right.background"
          label="Background color"
          @color-changed="(event) => (colors.right.background = event)"
        />
      </div>
      <div v-show="editing">
        <hr />
        <h2>General</h2>
        <WidthPicker
          label="Left column width"
          :defaultWidth="leftColumnWidth"
          @width-changed="leftColumnWidth = $event"
        />
        <SelectInput
          label="Headlines thickness"
          @update-selection="headlineWeight = $event"
          :default-option="headlineWeight"
          :options="[
            { name: 'Thin', value: '300' },
            { name: 'Medium', value: '400' },
            { name: 'Thick', value: '600' }
          ]"
        />
        <ToggleSwitch @switch-toogled="toggleImageDisplay" label="Show image" />
        <SelectInput
          label="Photo shape"
          @update-selection="imageShape = $event"
          :default-option="imageShape"
          :options="[
            { name: 'Round', value: 'round' },
            { name: 'Square', value: 'square' }
          ]"
        />
        <SelectInput
          label="Photo shape"
          @update-selection="imageShape = $event"
          :default-option="imageShape"
          :options="[
            { name: 'Round', value: 'round' },
            { name: 'Square', value: 'square' }
          ]"
        />

        <ImgUpload @image-changed="imageUrl = $event" />
      </div>
    </SidebarMenu>

    <div id="resume" class="d-flex" :class="{ 'edit-off': !editing }" :style="cssVariables">
      <div class="left-col">
        <ResumeSection>
          <img
            v-show="showImage"
            :src="imageUrl"
            class="profile-pic"
            :class="{ cirle: imageShape === 'round' }"
            alt="profile picture"
          />

          <SectionHeadline
            :editing="editing"
            :headlines="headlines[0]"
            @headline-edited="(val) => updateHeadline(val, 0)"
          />

          <span># {{ personnalInfo.name }}</span>
          <div :contenteditable="editing" @blur="updatePersonnalInfo($event, 'introText')">
            {{ personnalInfo.introText }}
          </div>
        </ResumeSection>

        <ResumeSection>
          <SectionHeadline
            :editing="editing"
            :headlines="headlines[1]"
            @headline-edited="(val) => updateHeadline(val, 1)"
          />
          <ContactInfo
            :editing="editing"
            :contact="contact"
            :icon-color="colors.left.highlight"
            @edit="(val, key) => updateContact(val, key)"
          />
        </ResumeSection>

        <ResumeSection>
          <SectionHeadline
            :editing="editing"
            :headlines="headlines[2]"
            @headline-edited="(val) => updateHeadline(val, 2)"
          />
          <ul>
            <li
              v-for="(skill, index) in skills"
              :key="index"
              :contenteditable="editing"
              @blur="updateSkill($event, index)"
            >
              {{ skill }}
            </li>
          </ul>
          <div v-if="!skills.length">No more item to remove</div>
          <EditButtons @add-click="skills.push('new entry')" @remove-click="skills.pop()" />
        </ResumeSection>

        <ResumeSection>
          <SectionHeadline
            :editing="editing"
            :headlines="headlines[3]"
            @headline-edited="(val) => updateHeadline(val, 3)"
          />

          <ul>
            <li
              v-for="(hlItem, index) in highlights"
              :key="index"
              :contenteditable="editing"
              @blur="updateHighlights($event, index)"
            >
              {{ hlItem }}
            </li>
          </ul>
          <div v-if="!highlights.length">No more item to remove</div>
          <EditButtons @add-click="highlights.push('new entry')" @remove-click="highlights.pop()" />
        </ResumeSection>
      </div>

      <div class="right-col">
        <div
          class="personal-name"
          :spellcheck="false"
          :contenteditable="editing"
          @blur="updatePersonnalInfo($event, 'name')"
        >
          {{ personnalInfo.name }}
        </div>
        <div
          class="personal-title"
          :contenteditable="editing"
          @blur="updatePersonnalInfo($event, 'title')"
        >
          {{ personnalInfo.title }}
        </div>

        <ResumeSection>
          <div class="d-flex justify-content-between">
            <SectionHeadline
              :editing="editing"
              :headlines="headlines[4]"
              @headline-edited="(val) => updateHeadline(val, 4)"
            />
            <EditButtons @add-click="addExperience" :show-remove-btn="false" />
          </div>

          <div v-if="!experience.length">Add an experience</div>
          <div v-for="(exp, index) in experience" :key="index" class="inner-section">
            <div class="inner-section-heading">
              <span :contenteditable="editing" @blur="updateExperience($event, 'title', index)">
                {{ exp.title }}
              </span>
              <EditButtons @remove-click="removeExperience(index)" :show-add-btn="false" />
            </div>
            <div class="d-flex justify-content-between">
              <div>
                <span
                  :contenteditable="editing"
                  @blur="updateExperience($event, 'company', index)"
                  >{{ exp.company }}</span
                >,
                <span
                  :contenteditable="editing"
                  @blur="updateExperience($event, 'location', index)"
                  >{{ exp.location }}</span
                >
              </div>
              <div :contenteditable="editing" @blur="updateExperience($event, 'date', index)">
                {{ exp.date }}
              </div>
            </div>
            <ul>
              <li
                v-for="(desc, innerIndex) in exp.description"
                :key="innerIndex"
                :contenteditable="editing"
                @blur="updateExperienceDescription($event, index, innerIndex)"
              >
                {{ desc }}
              </li>
            </ul>

            <div v-if="!exp.description.length">Add some description</div>
            <EditButtons
              :show-remove-btn="!!exp.description.length"
              @add-click="exp.description.push('new entry')"
              @remove-click="exp.description.pop()"
            />
          </div>
        </ResumeSection>

        <ResumeSection>
          <div class="d-flex justify-content-between">
            <SectionHeadline
              :editing="editing"
              :headlines="headlines[5]"
              @headline-edited="(val) => updateHeadline(val, 5)"
            />
            <EditButtons @add-click="addEducation" :show-remove-btn="false" />
          </div>
          <div v-if="!education.length">Add an education</div>
          <div v-for="(item, index) in education" :key="index" class="inner-section">
            <div class="inner-section-heading">
              <span :contenteditable="editing" @blur="updateEducation($event, 'title', index)">{{
                item.title
              }}</span>
              <EditButtons @remove-click="removeEducation(index)" :show-add-btn="false" />
            </div>
            <div class="d-flex justify-content-between">
              <div>
                <span
                  :contenteditable="editing"
                  @blur="updateEducation($event, 'university', index)"
                >
                  {{ item.university }} </span
                >,
                <span :contenteditable="editing" @blur="updateEducation($event, 'location', index)">
                  {{ item.location }}
                </span>
              </div>

              <div :contenteditable="editing" @blur="updateEducation($event, 'date', index)">
                {{ item.date }}
              </div>
            </div>
            <ul>
              <li
                v-for="(desc, innerIndex) in item.description"
                :key="innerIndex"
                :contenteditable="editing"
                @blur="updateEducationDescription($event, index, innerIndex)"
              >
                {{ desc }}
              </li>
            </ul>
            <div v-if="!item.description.length">Add some description</div>
            <EditButtons
              :show-remove-btn="!!item.description.length"
              @add-click="item.description.push('new entry')"
              @remove-click="item.description.pop()"
            />
          </div>
        </ResumeSection>
      </div>
    </div>
  </main>
</template>

<style scoped>
#resume {
  box-shadow:
    rgba(50, 50, 93, 0.25) 0px 13px 27px -5px,
    rgba(0, 0, 0, 0.3) 0px 8px 16px -8px;
  width: 210mm;
  margin-left: auto;
}

#resume.edit-off {
  /* DIN A4 standard paper size. commonly used for resumes
  For North America letter size use width: 8.5in; height: 11in; */
  height: 297mm;
}

@media (min-width: 1350px) {
  #resume {
    margin-left: 0;
  }
}

@media (min-width: 1600px) {
  #resume {
    margin-left: auto;
    margin-right: auto;
  }
}

.left-col {
  background-color: var(--background-color-left);
  color: var(--text-color-left);
  border-right: 1px solid var(--highlight-color-left);
  width: var(--left-column-width);
  padding: 30px;
}

.right-col {
  background-color: var(--background-color-right);
  color: var(--text-color-right);
  width: var(--right-column-width);
  padding: 30px;
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
  border: 2px solid var(--highlight-color-left);
  margin-bottom: 20px;
  object-fit: cover;
  margin-left: auto;
  margin-right: auto;
  border-radius: 5px;
}

.cirle {
  border-radius: 50%;
  border: 5px solid var(--highlight-color-left);
}

.inner-section {
  margin-bottom: 20px;
}

.inner-section-heading {
  display: flex;
  align-items: start;
  justify-content: space-between;
  margin-bottom: 10px;
}
</style>
