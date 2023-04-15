<script setup lang="ts">
const props = defineProps<{ name: string }>()
const router = useRouter()
const user = useUserStore()
const { t } = useI18n()

const formData = ref({
  foodType: '',
  healthLevel: '',
  mealTime: '',
})

const apiData = ref(null)

async function fetchData() {
  const response = await axios.get('https://jsonplaceholder.typicode.com/todos/1')
  apiData.value = response.data
}

function submitForm() {
// console.log('Form submitted:', formData.value);
}

// TODO: later this will come from imported list or list in db save by user
const ingredients = [
  'salt',
  'pepper',
  'red thai chili paste',
  'sriracha sauce',
  'tortilla',
  'black beans',
  'sugar',
]

watchEffect(() => {
  user.setNewName(props.name)
})
</script>

<template>
  <div>
    <div text-4xl>
      <div i-carbon-pedestrian inline-block />
    </div>
    <p>
      {{ t('intro.hi', { name: props.name }) }}
    </p>

    <p text-sm opacity-75>
      <em>{{ t('intro.dynamic-route', { name: props.name }) }}</em>
    </p>

    <template v-if="user.otherNames.length">
      <p mt-4 text-sm>
        <span opacity-75>{{ t('intro.aka') }}:</span>
        <ul>
          <li v-for="otherName in user.otherNames" :key="otherName">
            <RouterLink :to="`/hi/${otherName}`" replace>
              {{ otherName }}
            </RouterLink>
          </li>
        </ul>
      </p>
    </template>

    <div>
      <h1>Recipe creation form</h1>
      <form @submit.prevent="submitForm">
        <div>
          <label for="food-type">Choose a food type:</label>
          <select id="food-type" v-model="formData.foodType" name="foodType">
            <option value="">
              --Please choose an option--
            </option>
            <option value="asian">
              Asian
            </option>
            <option value="south-american">
              South American
            </option>
            <option value="indian">
              Indian
            </option>
            <option value="italian">
              Italian
            </option>
            <option value="american">
              American
            </option>
            <option value="mexican">
              Mexican
            </option>
            <option value="japanese">
              Japanese
            </option>
            <option value="chinese">
              Chinese
            </option>
            <option value="thai">
              Thai
            </option>
            <option value="french">
              French
            </option>
            <option value="spanish">
              Spanish
            </option>
            <option value="greek">
              Greek
            </option>
          </select>
        </div>
        <div>
          <label for="health-level">Healthiness level:</label>
          <select id="health-level" v-model="formData.healthLevel" name="healthLevel">
            <option value="">
              --Please choose an option--
            </option>
            <option value="1">
              1 (Least healthy)
            </option>
            <option value="2">
              2
            </option>
            <option value="3">
              3
            </option>
            <option value="4">
              4
            </option>
            <option value="5">
              5 (Healthiest)
            </option>
          </select>
        </div>
        <div>
          <label for="meal-time">Meal time:</label>
          <select id="meal-time" v-model="formData.mealTime" name="mealTime">
            <option value="">
              --Please choose an option--
            </option>
            <option value="breakfast">
              Breakfast
            </option>
            <option value="brunch">
              Brunch
            </option>
            <option value="lunch">
              Lunch
            </option>
            <option value="snack">
              Snack
            </option>
            <option value="dinner">
              Dinner
            </option>
            <option value="dessert">
              Dessert
            </option>
          </select>
        </div>
        <button m="t6" text-sm btn type="submit">
          Submit
        </button>
      </form>
    </div>

    <div>
      <button
        m="3 t6" text-sm btn
        @click="router.back()"
      >
        {{ t('button.back') }}
      </button>
    </div>
  </div>
</template>
