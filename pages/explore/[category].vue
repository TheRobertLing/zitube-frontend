<script setup lang="ts">
import {
  Breadcrumb,
  BreadcrumbItem,
  BreadcrumbLink,
  BreadcrumbList,
  BreadcrumbPage,
  BreadcrumbSeparator,
} from '@/components/ui/breadcrumb'
import { ChevronLeft, ChevronRight, ChevronsLeft, ChevronsRight } from 'lucide-vue-next'
import {
  PaginationEllipsis,
  PaginationFirst,
  PaginationLast,
  PaginationList,
  PaginationListItem,
  PaginationNext,
  PaginationPrev,
  PaginationRoot,
} from 'reka-ui'
import { Skeleton } from '@/components/ui/skeleton'
import defaultthumbnail from '@/assets/images/defaulthumbnail.png'

import {
  Card,
  CardContent,
  CardDescription,
  CardFooter,
  CardHeader,
  CardTitle,
} from '@/components/ui/card'
import { Separator } from '@/components/ui/separator'

const route = useRoute()
const category: string =
  (route.params.category as string).charAt(0).toUpperCase() +
  (route.params.category as string).slice(1)

const currentPage = ref<number>(Number(route.query.page || 1))

const isLoading = ref<boolean>(true)
</script>

<template>
  <main class="min-h-screen px-4 py-4">
    <!-- Navigation -->
    <Breadcrumb>
      <BreadcrumbList>
        <BreadcrumbItem>
          <BreadcrumbLink href="/"> Home </BreadcrumbLink>
        </BreadcrumbItem>
        <BreadcrumbSeparator />
        <BreadcrumbItem>
          <BreadcrumbLink href="/explore"> Explore </BreadcrumbLink>
        </BreadcrumbItem>
        <BreadcrumbSeparator />
        <BreadcrumbItem>
          <BreadcrumbPage>
            {{ category }}
          </BreadcrumbPage>
        </BreadcrumbItem>
      </BreadcrumbList>
    </Breadcrumb>

    <!-- Video's section -->
    <section>
      <h1 class="mt-8 mb-6 text-4xl font-bold">Category: {{ category }}</h1>

      <div class="grid grid-cols-1 gap-6 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4">
        <div class="flex flex-col space-y-3" v-for="i in 12" :key="i">
          <Skeleton class="aspect-video w-full rounded-xl" />
          <div class="space-y-2">
            <Skeleton class="h-4 w-full" />
            <Skeleton class="h-4 w-full" />
            <Skeleton class="h-4 w-full" />
          </div>
        </div>

        <Card class="w-full cursor-pointer overflow-hidden rounded-xl py-0 shadow-md">
          <!-- Thumbnail with padding and rounding -->
          <div class="aspect-video">
            <img :src="defaultthumbnail" alt="Video Thumbnail" class="object-fit rounded-lg" />
          </div>

          <!-- Title + Description -->
          <CardHeader class="space-y-1 px-6">
            <CardTitle class="line-clamp-2 text-lg">How to Never Get Rickrolled Again</CardTitle>
            <CardDescription class="text-sm text-muted-foreground"
              >by Rick Astley · 3 mins ago</CardDescription
            >
          </CardHeader>

          <!-- Optional Content -->
          <CardContent class="px-6 pt-2">
            <p class="line-clamp-2 text-sm text-muted-foreground">
              Learn the ancient secrets of avoiding suspicious links and recognizing that beat drop
              before it's too late.
            </p>
          </CardContent>

          <!-- Badges -->
          <CardFooter class="flex flex-wrap gap-2 px-6 pt-2 pb-4">
            <span class="rounded-full bg-muted px-3 py-1 text-xs text-muted-foreground"
              >Tutorial</span
            >
            <span class="rounded-full bg-muted px-3 py-1 text-xs text-muted-foreground"
              >Subtitled</span
            >
            <span class="rounded-full bg-muted px-3 py-1 text-xs text-muted-foreground">4:20</span>
          </CardFooter>
        </Card>

        <Videocard
          thumbnail="https://img.youtube.com/vi/dQw4w9WgXcQ/hqdefault.jpg"
          title="How to Never Get Rickrolled Again"
          author="Rick Astley"
          time="3 mins ago"
          description="Learn the ancient secrets of avoiding suspicious links and recognizing that beat drop before it's too late."
          :badges="['Tutorial', 'Subtitled', '4:20']"
        />
      </div>
    </section>

    <Separator class="my-4" label="END OF PAGE" />

    <!-- Pagination -->
    <nav class="mt-8 flex justify-center">
      <PaginationRoot
        v-model:page="currentPage"
        :total="100"
        :sibling-count="1"
        :items-per-page="10"
        show-edges
        :default-page="1"
      >
        <PaginationList
          v-slot="{ items }"
          class="flex items-center gap-1 text-stone-700 dark:text-white"
        >
          <PaginationFirst
            class="flex h-9 w-9 cursor-pointer items-center justify-center rounded-lg bg-transparent transition hover:bg-white disabled:opacity-50 dark:hover:bg-stone-700/70"
          >
            <ChevronsLeft />
          </PaginationFirst>
          <PaginationPrev
            class="mr-4 flex h-9 w-9 cursor-pointer items-center justify-center rounded-lg bg-transparent transition hover:bg-white disabled:opacity-50 dark:hover:bg-stone-700/70"
          >
            <ChevronLeft />
          </PaginationPrev>
          <template v-for="(page, index) in items">
            <PaginationListItem
              v-if="page.type === 'page'"
              :key="index"
              class="h-9 w-9 cursor-pointer rounded-lg border transition hover:bg-white data-[selected]:!bg-[hsl(142.1_70.6%_45.3%)] data-[selected]:text-black data-[selected]:shadow-sm dark:border-stone-800 dark:hover:bg-stone-700/70"
              :value="page.value"
            >
              {{ page.value }}
            </PaginationListItem>
            <PaginationEllipsis
              v-else
              :key="page.type"
              :index="index"
              class="flex h-9 w-9 items-center justify-center"
            >
              &#8230;
            </PaginationEllipsis>
          </template>
          <PaginationNext
            class="ml-4 flex h-9 w-9 cursor-pointer items-center justify-center rounded-lg bg-transparent transition hover:bg-white disabled:opacity-50 dark:hover:bg-stone-700/70"
          >
            <ChevronRight />
          </PaginationNext>
          <PaginationLast
            class="flex h-9 w-9 cursor-pointer items-center justify-center rounded-lg bg-transparent transition hover:bg-white disabled:opacity-50 dark:hover:bg-stone-700/70"
          >
            <ChevronsRight />
          </PaginationLast>
        </PaginationList>
      </PaginationRoot>
    </nav>
  </main>
</template>

<style scoped></style>
