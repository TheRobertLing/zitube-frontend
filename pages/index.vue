<script setup lang="ts">
import { Button } from "@/components/ui/button";
import { Compass } from "lucide-vue-next";
</script>

<template>
  <div>
    <!-- Hero Section -->
    <div
      class="min-h-screen flex flex-col justify-center items-center text-center space-y-6 "
    >
      <h1
        class="scroll-m-20 text-4xl font-extrabold tracking-tight lg:text-5xl"
      >
        Welcome to ZiTube
      </h1>

      <p class="text-muted-foreground text-lg">
        Learn Chinese through media, one video at a time.
      </p>

      <NuxtLink to="/explore">
        <Button class="cursor-pointer">
          <Compass class="w-4 h-4" />
          Explore Videos
        </Button>
      </NuxtLink>
    </div>

    <!-- Intro to the Site -->
    <div class="bg-primary">

    </div>
  </div>
</template>

<style scoped>
</style>
