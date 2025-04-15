<script setup lang="ts">
import { Separator } from '@/components/ui/separator'
import {
  Breadcrumb,
  BreadcrumbItem,
  BreadcrumbLink,
  BreadcrumbList,
  BreadcrumbPage,
  BreadcrumbSeparator,
} from '@/components/ui/breadcrumb'
import gogogo出发咯 from '@/assets/images/gogogo出发咯.png'
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
          <BreadcrumbPage> About </BreadcrumbPage>
        </BreadcrumbItem>
      </BreadcrumbList>
    </Breadcrumb>

    <h1 class="mt-8 mb-6 text-4xl font-bold">About ZiTube</h1>

    <p class="mb-10 text-lg text-muted-foreground">
      ZiTube is a small project created to help people on their Chinese language learning journey by
      offering full translated transcripts complete with vocabulary search and contextual hints for
      videos that span across a large selection of content types. ZiTube also allows users to create
      Anki flashcard decks directly from video transcripts via the integrated Anki panel.
    </p>

    <Separator class="my-10" />

    <section class="mb-12">
      <h2 class="mb-3 text-2xl font-semibold">What ZiTube Does</h2>
      <p class="mb-4 text-muted-foreground">
        The goal of ZiTube enhances video watching for learners by offering:
      </p>
      <ul class="list-inside list-disc space-y-2 text-muted-foreground">
        <li>Videos with line-by-line Chinese subtitles</li>
        <li>Interactive translations and pinyin</li>
        <li>Contextual grammar and usage insights</li>
        <li>User-curated commentary and vocabulary highlights</li>
        <li>Anki support with an integrated vocabulary deck builder</li>
      </ul>
    </section>

    <Separator class="my-10" />

    <section class="mb-12">
      <h2 class="mb-3 text-2xl font-semibold">Roadmap</h2>
      <p class="mb-6 text-muted-foreground">
        The roadmap below outlines planned features for ZiTube. Items are grouped by timeline, but
        may shift based on feedback and priorities.
      </p>

      <!-- Short Term -->
      <div class="mb-8">
        <h3 class="mb-2 text-xl font-medium">Short Term</h3>
        <ul class="list-inside list-none space-y-2 text-muted-foreground">
          <li>✅ Public About & Contact pages</li>
          <li>✅ Static routing with progressive enhancement for login</li>
          <li>🔲 Basic user login system</li>
          <li>🔲 Interactive transcript + translations UX polish</li>
        </ul>
      </div>

      <!-- Medium Term -->
      <div class="mb-8">
        <h3 class="mb-2 text-xl font-medium">Medium Term</h3>
        <ul class="list-inside list-none space-y-2 text-muted-foreground">
          <li>🔲 User accounts with saved progress and word banks</li>
          <li>🔲 Upload system for creators to contribute content</li>
          <li>🔲 Search & filter system for video library</li>
        </ul>
      </div>

      <!-- Long Term -->
      <div>
        <h3 class="mb-2 text-xl font-medium">Long Term</h3>
        <ul class="list-inside list-none space-y-2 text-muted-foreground">
          <li>🔲 Smart features: dictionary popups, SRS review, tone-based sorting</li>
          <li>🔲 Speech input for pronunciation or shadowing practice</li>
          <li>🔲 Collaborative features (comments, community edits, voting)</li>
        </ul>
      </div>
    </section>

    <figure class="ml-auto mr-auto mt-10 w-1/2">
      <img :src="gogogo出发咯" alt="gogogo 出发咯" class="mb-2 rounded-md ml-auto mr-auto" />
      <figcaption class="text-center text-sm text-muted-foreground">
        Image Source:
        <a
          href="https://p3-pc-sign.douyinpic.com/tos-cn-i-0813/oIAAzFXXy8gJDfdA7fkEfcBuAEETBHAQZPWOII~tplv-dy-aweme-images:q75.webp?biz_tag=aweme_images&from=327834062&lk3s=138a59ce&s=PackSourceEnum_SEARCH&sc=image&se=false&x-expires=1747278000&x-signature=7ckNiHPwpVy0BLTMH8FRZPLkCNI%3D"
          target="_blank"
        >
          Click Me
        </a>
      </figcaption>
    </figure>
  </main>
</template>

<style scoped></style>
