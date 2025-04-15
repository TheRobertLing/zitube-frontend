<script setup lang="ts">
import type { NuxtError } from "#app";
import { ArrowLeft } from "lucide-vue-next";
import { Button } from "@/components/ui/button";
import error from "@/assets/images/error.gif";
import {
  Card,
  CardContent,
  CardDescription,
  CardFooter,
  CardHeader,
  CardTitle,
} from "@/components/ui/card";

const props = defineProps<{
  error: NuxtError;
}>();

const statusCode = props.error.statusCode || 500;
const message = props.error.message || "Something went wrong.";
</script>

<template>
  <div class="min-h-screen flex items-center justify-center">
    <Card class="mx-auto text-center">
      <CardHeader>
        <CardTitle>Error {{ statusCode }}</CardTitle>
        <CardDescription>
          Oops, this page doesn't exist or is under construction.
        </CardDescription>
      </CardHeader>

      <CardContent>
        <img :src="error" alt="Page Not Found" class="w-full rounded" />
      </CardContent>

      <CardFooter class="flex justify-center">
        <NuxtLink to="/" class="w-full">
          <Button class="w-full cursor-pointer">
            <ArrowLeft class="w-4 h-4" />
            Back to Home
          </Button>
        </NuxtLink>
      </CardFooter>
    </Card>
  </div>
</template>
