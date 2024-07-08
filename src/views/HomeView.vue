<script setup>
import HeroSections from "@/components/HeroSection.vue";
import HomeCards from "@/components/HomeCards.vue";
import JobListings from "@/components/JobListings.vue";
</script>

<template>
  <HeroSections />
  <HomeCards />
  <JobListings limit="3" :show-button="true" />
</template>
