<template>
  <v-app>
    <v-app-bar app fixed class="blue">
      <v-spacer />
      <v-toolbar-title>WEBSORT</v-toolbar-title>
      <v-spacer />
    </v-app-bar>

    <v-main>
      <v-container>
        <v-row justify="start" class="ma-2">
          <v-col cols="2" v-for="(item, id) in inputArray" :key="id">
            <v-text-field
              dense
              outlined
              v-model="inputArray[id]"
              :rules="[rules.number]"
              append-icon="mdi-close"
              @click:append="removeBox(id)"
              autofocus
            ></v-text-field>
          </v-col>
          <v-col cols="2">
            <v-btn icon @click="addBox"><v-icon>mdi-plus</v-icon></v-btn>
          </v-col>
        </v-row>
        <v-row class="ma-2">
          <v-btn block @click="sortArray" class="blue">SORT THIS ARRAY</v-btn>
        </v-row>
        <v-row class="ma-2">
          <h2>
            {{ sortedArray }}
          </h2>
        </v-row>
      </v-container>
    </v-main>

    <v-footer app fixed class="grey">
      <v-toolbar-title
        >Made by Nandeesh as a part of MLH-Local Hack Day
        Sprint</v-toolbar-title
      >
      <v-spacer />
      More at -
      <v-btn icon href="https://github.com/NandeeshG/" target="_blank"
        ><v-icon>mdi-github</v-icon></v-btn
      >
      <v-btn
        icon
        href="https://www.linkedin.com/in/nandeesh-gupta-05b43014a/"
        target="_blank"
        ><v-icon>mdi-linkedin</v-icon></v-btn
      >
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      inputArray: [],
      sortedArray: [],
      rules: {
        required: value => !!value || "Required.",
        counter: value => value.length <= 20 || "Max 20 characters",
        number: value => {
          const pattern = /^[0-9]+$/;
          return pattern.test(value) || "Number only.";
        }
      }
    };
  },
  methods: {
    sortArray() {
      this.sortedArray = this.inputArray.map(val => parseInt(val, 10));
      this.sortedArray.sort((a, b) => a - b); // For ascending sort
    },
    addBox() {
      this.inputArray.push(0);
    },
    removeBox(i) {
      this.inputArray.splice(i, 1);
    }
  }
};
</script>
