<template>
<DefaultLayout>
  <template #header>
    <Hero
      image-url="/flock-camera.jpeg"
      :opacity="0"
    />
  </template>
  
  <v-container>
    <h1 class="mt-0">What are ALPRs?</h1>
    <p>
      Automated License Plate Readers (ALPRs or LPRs) are AI-powered cameras that capture and analyze images of <b>all passing vehicles</b>, storing details like your car's <b>location, date, and time</b>. They also capture your car's <b>make, model, color</b>, and <b>identifying features</b> such as dents, roof racks, and bumper stickers, often turning these into <b>searchable data points</b>.
    </p>
    <p>
      These cameras collect data on millions of vehicles <b>regardless of whether the driver is suspected of a crime</b>. These systems are marketed as indispensable tools to fight crime, but they ignore the powerful tools police already have to track criminals, such as cell phone location data, <b>creating a loophole that doesn't require a warrant</b>.
    </p>

    <p>For a detailed explanation of how ALPRs are a threat to privacy, see this <a href="https://www.aclu.org/issues/privacy-technology/you-are-being-tracked" target="_blank">ACLU article</a> as well as this <a href="https://sls.eff.org/technologies/automated-license-plate-readers-alprs" target="_blank">EFF article</a> on ALPRs.</p>

    <v-divider class="my-12" />

    <h2 class="mb-8">
      <v-icon class="mr-2" color="primary">mdi-camera-outline</v-icon>
      What do they look like?
    </h2>
    <div class="mb-16 text-center">
      <v-btn size="large" color="primary" to="/identify">
        <v-icon left class="mr-2">mdi-image-search</v-icon>
        View ALPR Images
      </v-btn>
    </div>

    <v-divider class="my-12" />

    <h2>Why Should You Be Concerned</h2>
    <p class="mb-8 text-center">
      ALPRs invade your privacy and violate your civil liberties. Here's how:
    </p>

    <Dangers />

    <v-divider class="my-12" />

    <h2 class="mb-8">Frequently Asked Questions</h2>
    <FAQ />
    
    <v-divider class="my-12" />
    
    <SimilarProjects id="similar" />
  </v-container>
</DefaultLayout>
</template>

<script setup lang="ts">
import DefaultLayout from '@/layouts/DefaultLayout.vue';
import Hero from '@/components/layout/Hero.vue';
import Dangers from '@/components/Dangers.vue';
import FAQ from '@/components/FAQ.vue';
import SimilarProjects from '@/components/SimilarProjects.vue';
</script>

<style scoped>
h1, h2 {
  text-align: center;
}

.scrim {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  color: white;
  font-size: 1.5rem;
  font-weight: bold;
}

.image-close-btn {
  position: absolute;
  top: 0;
  right: 0;
  color: white;
  z-index: 100;
}

.scrim-text {
  text-transform: uppercase;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.25s;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
