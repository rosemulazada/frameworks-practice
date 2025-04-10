<script setup>
import { reactive } from 'vue'
import axios from 'axios'
import router from '@/router'
import { useToast } from 'vue-toastification'

const form = reactive({
  type: 'Full-Time',
  title: '',
  description: '',
  salary: '',
  location: '',
  company: {
    name: '',
    description: '',
    contactEmail: '',
    contactPhone: '',
  },
})

const toast = useToast()

const handleSubmit = async () => {
  const newJob = {
    title: form.title,
    type: form.type,
    description: form.description,
    salary: form.salary,
    location: form.location,
    company: {
      name: form.company.name,
      description: form.company.description,
      contactEmail: form.company.contactEmail,
      contactPhone: form.company.contactPhone,
    },
  }

  try {
    const response = await axios.post(`/api/jobs/`, newJob)
    toast.success('Job added successfully.')
    router.push(`/jobs/${response.data.id}`)
  } catch (error) {
    console.error('Error fetching job', error)
    toast.error('Error adding job', error)
  }
}
</script>

<template>
  <section class="bg-green-50">
    <div class="container m-auto max-w-2xl py-24">
      <div class="bg-white px-6 py-8 mb-4 shadow-md rounded-md border m-4 md:m-0">
        <form @submit.prevent="handleSubmit">
          <h2 class="text-3xl text-center font-semibold mb-6">Add Job</h2>

          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2" for="type">Job Type</label>
            <select
              id="type"
              v-model="form.type"
              class="border rounded w-full py-2 px-3"
              name="type"
              required
            >
              <option value="Full-Time">Full-Time</option>
              <option value="Part-Time">Part-Time</option>
              <option value="Remote">Remote</option>
              <option value="Internship">Internship</option>
            </select>
          </div>

          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2">Job Listing Name</label>
            <input
              id="name"
              v-model="form.title"
              class="border rounded w-full py-2 px-3 mb-2"
              name="name"
              placeholder="eg. Beautiful Apartment In Miami"
              required
              type="text"
            />
          </div>
          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2" for="description">Description</label>
            <textarea
              id="description"
              v-model="form.description"
              class="border rounded w-full py-2 px-3"
              name="description"
              placeholder="Add any job duties, expectations, requirements, etc"
              rows="4"
            ></textarea>
          </div>

          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2" for="type">Salary</label>
            <select
              id="salary"
              v-model="form.salary"
              class="border rounded w-full py-2 px-3"
              name="salary"
              required
            >
              <option value="Under $50K">under $50K</option>
              <option value="$50K - $60K">$50 - $60K</option>
              <option value="$60K - $70K">$60 - $70K</option>
              <option value="$70K - $80K">$70 - $80K</option>
              <option value="$80K - $90K">$80 - $90K</option>
              <option value="$90K - $100K">$90 - $100K</option>
              <option value="$100K - $125K">$100 - $125K</option>
              <option value="$125K - $150K">$125 - $150K</option>
              <option value="$150K - $175K">$150 - $175K</option>
              <option value="$175K - $200K">$175 - $200K</option>
              <option value="Over $200K">Over $200K</option>
            </select>
          </div>

          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2"> Location </label>
            <input
              id="location"
              v-model="form.location"
              class="border rounded w-full py-2 px-3 mb-2"
              name="location"
              placeholder="Company Location"
              required
              type="text"
            />
          </div>

          <h3 class="text-2xl mb-5">Company Info</h3>

          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2" for="company">Company Name</label>
            <input
              id="company"
              v-model="form.company.name"
              class="border rounded w-full py-2 px-3"
              name="company"
              placeholder="Company Name"
              type="text"
            />
          </div>

          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2" for="company_description"
              >Company Description</label
            >
            <textarea
              id="company_description"
              v-model="form.company.description"
              class="border rounded w-full py-2 px-3"
              name="company_description"
              placeholder="What does your company do?"
              rows="4"
            ></textarea>
          </div>

          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2" for="contact_email"
              >Contact Email</label
            >
            <input
              id="contact_email"
              v-model="form.company.contactEmail"
              class="border rounded w-full py-2 px-3"
              name="contact_email"
              placeholder="Email address for applicants"
              required
              type="email"
            />
          </div>
          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2" for="contact_phone"
              >Contact Phone</label
            >
            <input
              id="contact_phone"
              v-model="form.company.contactPhone"
              class="border rounded w-full py-2 px-3"
              name="contact_phone"
              placeholder="Optional phone for applicants"
              type="tel"
            />
          </div>

          <div>
            <button
              class="bg-green-500 hover:bg-green-600 text-white font-bold py-2 px-4 rounded-full w-full focus:outline-none focus:shadow-outline"
              type="submit"
            >
              Add Job
            </button>
          </div>
        </form>
      </div>
    </div>
  </section>
</template>
