<template>
  <v-sheet min-width="240">
    <v-list density="compact">
      <v-list-item v-if="isFaceRecognition">
        <v-icon start>mdi-face-recognition</v-icon> <b>Face Recognition</b>
      </v-list-item>
      <v-list-item>
        <v-icon start>mdi-car</v-icon> <b>License Plate</b>
      </v-list-item>
      <v-list-item v-if="isFaceRecognition">
        <v-icon start>mdi-adjust</v-icon> <b>Omnidirectional</b>
      </v-list-item>
      <v-list-item v-else>
        <v-icon start>mdi-cctv</v-icon> <b>Directional {{ alpr.properties.tags.direction ? `(${degreesToCardinal(parseInt(alpr.properties.tags.direction))})` : '' }}</b>
      </v-list-item>
      <v-list-item>
        <v-icon start>mdi-domain</v-icon> <b>
          <span v-if="alpr.properties.tags.brand">
            {{ alpr.properties.tags.brand }}
          </span>
          <span v-else>
            Unknown Brand
            <!-- <v-btn :href="osmNodeUrl" variant="text" flat size="x-small" color="warning" target="_blank">
              <v-icon start size="small">mdi-pencil</v-icon>Fix
            </v-btn> -->
          </span>
        </b>
      </v-list-item>
      <v-list-item>
        <v-icon start>mdi-police-badge</v-icon> <b>
          <span v-if="alpr.properties.tags.operator">
            {{ alpr.properties.tags.operator }}
          </span>
          <span v-else>
            Unknown Operator
            <!-- <v-btn :href="osmNodeUrl" variant="text" flat size="x-small" color="warning" target="_blank">
              <v-icon start size="small">mdi-pencil</v-icon>Fix
            </v-btn> -->
          </span>
        </b>
      </v-list-item>
    </v-list>

    <div class="text-center text-grey-darken-1">
      node/{{ alpr.properties.id }}
    </div>
    <!-- <v-data-table density="compact" hide-default-header hide-default-footer disable-sort :items="kvTags" /> -->
  </v-sheet>
</template>

<script setup lang="ts">
import { defineProps, computed } from 'vue';
import type { PropType } from 'vue';
import type { GeoJSONPoint } from '@/types';

const props = defineProps({
  alpr: {
    type: Object as PropType<GeoJSONPoint>,
    required: true
  }
});

const valueTransformations: { [key: string]: (value: string) => string } = {
  direction: (value: string) => `${degreesToCardinal(parseInt(value))} ${value}º`
};

const whitelistedTags = ['brand', 'camera:mount', 'camera:type', 'direction', 'operator'];

const isFaceRecognition = computed(() => props.alpr.properties.tags.brand === 'Avigilon');
const osmNodeUrl = computed(() => `/node/${props.alpr.properties.id}`);

const kvTags = computed(() => {
  return Object.entries(props.alpr.properties.tags)
    .filter(([key]) => whitelistedTags.includes(key))
    .map(([key, value]) => ({ key, value: valueTransformations[key]?.(value) ?? value }));
});

function degreesToCardinal(degrees: number): string {
  const cardinals = ['North', 'Northeast', 'East', 'Southeast', 'South', 'Southwest', 'West', 'Northwest'];
  return cardinals[Math.round(degrees / 45) % 8];
}
</script>
