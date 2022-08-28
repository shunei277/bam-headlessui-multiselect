<template>
  <div class="w-full">
    <Combobox
      v-model="selectedOptions"
      multiple
    >
      <div class="relative mt-1">
        <div
          class="
            relative w-full cursor-default overflow-hidden rounded-lg bg-white
            p-4 gap-2 flex flex-wrap text-left shadow-md
          "
        >
          <span
            v-for="selectedOption in selectedOptions"
            :key="selectedOption.id"
            class="bg-teal-600 text-white px-2 py-1 inline-block"
          >{{ selectedOption.name }}
            <span
              class="pl-1"
              @click="removeItem(selectedOption)"
            >
              X
            </span>
          </span>
          <ComboboxInput
            class="border-none py-2 pl-3 mr-10 text-sm leading-5 text-gray-900 flex-grow"
            :display-value="(option) => option.name"
            @change="query = $event.target.value"
          />
          <ComboboxButton
            class="absolute inset-y-0 right-0 flex items-center pr-2"
          >
            <SelectorIcon
              class="h-5 w-5 text-gray-400"
              aria-hidden="true"
            />
          </ComboboxButton>
        </div>
        <TransitionRoot
          leave="transition ease-in duration-100"
          leave-from="opacity-100"
          leave-to="opacity-0"
        >
          <ComboboxOptions
            class="
              absolute mt-1 max-h-60 w-full overflow-auto rounded-md bg-white py-1
              text-base shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none sm:text-sm
            "
          >
            <ComboboxOption
              v-for="person in options"
              :key="person.id"
              v-slot="{ selected, active }"
              as="template"
              :value="person"
            >
              <li
                class="relative cursor-default select-none py-2 pl-10 pr-4"
                :class="{
                  'bg-teal-600 text-white': active,
                  'text-gray-900': !active,
                }"
              >
                <span
                  class="block truncate"
                  :class="{ 'font-medium': selected, 'font-normal': !selected }"
                >
                  {{ person.name }}
                </span>
                <span
                  v-if="selected"
                  class="absolute inset-y-0 left-0 flex items-center pl-3"
                  :class="{ 'text-white': active, 'text-teal-600': !active }"
                >
                  <CheckIcon
                    class="h-5 w-5"
                    aria-hidden="true"
                  />
                </span>
              </li>
            </ComboboxOption>
          </ComboboxOptions>
        </TransitionRoot>
      </div>
    </Combobox>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';
import {
  Combobox,
  ComboboxInput,
  ComboboxButton,
  ComboboxOptions,
  ComboboxOption,
  TransitionRoot,
} from '@headlessui/vue';
import { CheckIcon, SelectorIcon } from '@heroicons/vue/solid';

const options = [
  { id: 1, name: '日本，東京' },
  { id: 2, name: '日本，神奈川' },
  { id: 3, name: '日本，大阪' },
  { id: 4, name: '日本，福岡' },
  { id: 5, name: 'アメリカ，カリフォルニア' },
  { id: 6, name: 'イギリス，マンチェスター' },
];

const selectedOptions = ref<{id: number, name: string}[]>([]);
const query = ref('');
const removeItem = (item: {id: number, name: string}) => {
  selectedOptions.value = selectedOptions.value.filter(
    (value) => value.id !== item.id,
  );
};
</script>
