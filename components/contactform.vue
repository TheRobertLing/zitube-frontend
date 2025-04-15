<script setup lang="ts">
import { useForm } from 'vee-validate'
import { toTypedSchema } from '@vee-validate/zod'
import { z } from 'zod'
import { FormField, FormItem, FormLabel, FormControl, FormMessage } from '@/components/ui/form'
import { Input } from '@/components/ui/input'
import { Textarea } from '@/components/ui/textarea'
import { Button } from '@/components/ui/button'

type Web3FormsResponse = {
  status: number
  message: string
}

const contactFormSchema = toTypedSchema(
  z.object({
    name: z.string().min(1, 'Name is required'),
    email: z.string().nonempty('Field is required').email('Invalid email address'),
    message: z.string().min(10, 'Message must be at least 10 characters'),
  }),
)

const { handleSubmit } = useForm({
  validationSchema: contactFormSchema,
})

const result = ref<string>('')
const status = ref<'loading' | 'success' | 'error' | ''>('')

const form = ref({
  access_key: 'f786d4e2-21fb-4ad2-b625-eefba9666c66',
  subject: 'New Submission from Web3Forms',
  name: '',
  email: '',
  message: '',
})

const submitForm = handleSubmit(async (values) => {
  try {
    status.value = 'loading'
    const response = await $fetch<Web3FormsResponse>('https://api.web3forms.com/submit', {
      method: 'POST',
      body: form.value,
    })

    result.value = response.message
    if (response.status === 200) {
      status.value = 'success'
    } else {
      status.value = 'error'
    }
  } catch (error) {
    status.value = 'error'
    result.value = 'Something went wrong!'
  } finally {
    form.value.name = ''
    form.value.email = ''
    form.value.message = ''

    setTimeout(() => {
      result.value = ''
      status.value = ''
    }, 5000)
  }
})
</script>

<template>
  <div class="flex w-full flex-col items-center justify-center">
    <h1 class="mb-2 text-3xl font-bold">Contact Form</h1>
    <p class="mb-6 max-w-md text-center text-muted-foreground">
      Have a question or want to get in touch? Fill out the form below and I'll get back to you as
      soon as possible.
    </p>

    <form class="w-full max-w-xl space-y-6" @submit.prevent="submitForm">
      <FormField name="name" v-slot="{ componentField }">
        <FormItem>
          <FormLabel>Name</FormLabel>
          <FormControl>
            <Input placeholder="Jane Doe" v-bind="componentField" />
          </FormControl>
          <FormMessage />
        </FormItem>
      </FormField>

      <FormField name="email" v-slot="{ componentField }">
        <FormItem>
          <FormLabel>Email</FormLabel>
          <FormControl>
            <Input placeholder="you@example.com" v-bind="componentField" />
          </FormControl>
          <FormMessage />
        </FormItem>
      </FormField>

      <FormField name="message" v-slot="{ componentField }">
        <FormItem>
          <FormLabel>Message</FormLabel>
          <FormControl>
            <Textarea placeholder="Enter your message..." rows="4" v-bind="componentField" />
          </FormControl>
          <FormMessage />
        </FormItem>
      </FormField>

      <Button type="submit" class="w-full" :disabled="status === 'loading'">
        {{ status === 'loading' ? 'Sending...' : 'Send Message' }}
      </Button>
    </form>
  </div>
</template>
