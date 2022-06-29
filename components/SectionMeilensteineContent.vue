<template>
  <div>
    <Title>{{section.title}}</Title>
    <div v-for="(element, index) in section.content" :key="'content' + index" style="break-inside: avoid">
      <div class="flex">
        <div class="w-1_5 flex-shrink-0 flex-grow-0 flex items-start justify-center">
          <div
            :style="{ backgroundColor: color }"
            class="w-1 h-1 text-base mt-02 rounded-xs flex-shrink-0"
          ></div>
        </div>
        <div class="flex-grow mb-05">
          <div :style="{ color: color }" class="text-bigger">
            {{ element.heading }}
          </div>
          <div v-if="element.subheading" class="text-sm">
            {{ element.subheading }}
          </div>
        </div>
      </div>
      <div>
        <div v-for="(milestone, idx) in element.milestones" :key="index + 'milestone' + idx">
          <div class="flex">
            <div class="w-1_5 flex-shrink-0 flex-grow-0 flex items-start justify-center relative">
              <div
                :style="{
                  backgroundImage: `url(${require('~/static/dot.png')})`,
                  backgroundRepeat: 'no-repeat',
                  backgroundSize: '100% 100%',
                }"
                class="w-1 h-1 text-base mt-01 rounded-xs flex-shrink-0"
              ></div>
              <div
                v-if="idx != element.milestones.length - 1"
                :style="{
                  backgroundImage: `url(${require('~/static/line-vertical.png')})`,
                  backgroundRepeat: 'no-repeat',
                  backgroundSize: '100% 100%',
                }"
                class="w-1px h-full absolute left-1/2 top-03 transform -translate-1/2"
              ></div>
            </div>
            <div class="flex-grow mb-05">
              <div class="text-sm">
                {{ milestone.date }}
              </div>
              <div class="text-bigger">
                {{ milestone.title }}
              </div>

            <div>
              <div
                v-for="(project, i) in milestone.projects"
                :key="index + idx + 'project' + i"
                class="mt-03"
              >
                <div class="text-base font-bold">
                  {{ project.heading }}
                </div>
                <div v-html="project.text" class="text-base"></div>
              </div>
            </div>
            </div>

          </div>

        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import { mapGetters } from "vuex";
  export default {
    props: {
      section: {
        type: Object,
        required: true,
      },
    },

    computed: {
      ...mapGetters(["color"]),
    },
  };
</script>

<style></style>
