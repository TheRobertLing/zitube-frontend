<script setup lang="ts">
import {
  Breadcrumb,
  BreadcrumbItem,
  BreadcrumbLink,
  BreadcrumbList,
  BreadcrumbPage,
  BreadcrumbSeparator,
} from '@/components/ui/breadcrumb'
import {
  Card,
  CardContent,
  CardDescription,
  CardFooter,
  CardHeader,
  CardTitle,
} from '@/components/ui/card'
import { Separator } from '@/components/ui/separator'

const categories = ref<string[]>([
  'All',
  'Technology',
  'Animation',
  'Pop Culture',
  'Drama',
  'Music',
  'Education',
  'Movies',
  'Gaming',
  'Misc',
])

const handleClick = (category: string) => {
  return navigateTo({
    path: `/explore/${category.toLowerCase()}`,
    query: {
      page: 1,
    },
  })
}
</script>

<template>
  <main class="min-h-screen px-4 py-4">
    <Breadcrumb>
      <BreadcrumbList>
        <BreadcrumbItem>
          <BreadcrumbLink href="/"> Home </BreadcrumbLink>
        </BreadcrumbItem>
        <BreadcrumbSeparator />
        <BreadcrumbItem>
          <BreadcrumbPage> Explore </BreadcrumbPage>
        </BreadcrumbItem>
      </BreadcrumbList>
    </Breadcrumb>

    <h1 class="mt-8 mb-6 text-4xl font-bold">Categories</h1>

    <p class="mb-10 text-lg text-muted-foreground">
      Below is a curated list of video categories, aimed at covering a wide range of genres and
      real-world topics. From tech and culture to entertainment and everyday life, there's something
      for everyone — hopefully. If not, feel free to send suggestions.
    </p>

    <section class="grid grid-cols-1 gap-6 sm:grid-cols-2 md:grid-cols-3">
      <Card
        v-for="(category, index) in categories"
        :key="index"
        class="cursor-pointer transition hover:scale-103"
        @click="handleClick(category)"
      >
        <CardHeader>
          <CardTitle class="break-all">{{ category }}</CardTitle>
          <CardDescription></CardDescription>
        </CardHeader>
        <CardContent></CardContent>
        <CardFooter></CardFooter>
      </Card>
    </section>

    <Separator class="my-4" label="END" />
  </main>
</template>

<style scoped></style>
