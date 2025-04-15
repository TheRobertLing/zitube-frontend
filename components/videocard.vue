<script setup lang="ts">
import defaulthumbnail from '@/assets/images/defaulthumbnail.png'
import {
  Card,
  CardContent,
  CardDescription,
  CardFooter,
  CardHeader,
  CardTitle,
} from '@/components/ui/card'

defineProps<{
  thumbnail: string // The URL
  title: string
  author: string
  time: string
  description: string
  badges: string[]
}>()

const imageRef = useTemplateRef('thumbnail')

const onImageError = (): void => {
  if (imageRef.value) {
    imageRef.value.src = defaulthumbnail
  }
}

const handleClick = (): void => {

}
</script>

<template>
  <Card class="w-full cursor-pointer overflow-hidden rounded-xl py-0 shadow-md" @click="handleClick()">
    <!-- Thumbnail -->
    <div class="aspect-video overflow-hidden">
      <img
        :src="thumbnail"
        :alt="title"
        class="h-full w-full object-cover"
        @error="onImageError"
        ref="thumbnail"
      />
    </div>

    <!-- Title + Description -->
    <CardHeader class="space-y-1 px-6">
      <CardTitle class="line-clamp-2 text-lg">{{ title }}</CardTitle>
      <CardDescription class="text-sm text-muted-foreground">
        by {{ author }} · {{ time }}
      </CardDescription>
    </CardHeader>

    <!-- Optional Content -->
    <CardContent class="px-6 pt-2">
      <p class="line-clamp-2 text-sm text-muted-foreground">
        {{ description }}
      </p>
    </CardContent>

    <!-- Badges -->
    <CardFooter class="flex flex-wrap gap-2 px-6 pt-2 pb-4">
      <span
        v-for="(badge, index) in badges"
        :key="index"
        class="rounded-full bg-muted px-3 py-1 text-xs text-muted-foreground"
      >
        {{ badge }}
      </span>
    </CardFooter>
  </Card>
</template>
