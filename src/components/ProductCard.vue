<template>
    <b-card no-body class="overflow-hidden" style="max-width: 540px;">
    <b-row no-gutters>
      <b-col md="6">
        <b-card-img src="https://picsum.photos/400/400/?image=20" alt="Image" class="rounded-0"></b-card-img>
      </b-col>
      <b-col md="6">
        <b-card-body title="Horizontal Card">
          <b-card-text>
            This is a wider card with supporting text as a natural lead-in to additional content.
            This content is a little bit longer.
          </b-card-text>
        </b-card-body>
      </b-col>
      <b-col md="12">
          <b-form-group
      v-slot="{ ariaDescribedby }"
    >
      <b-form-radio-group
        id="btn-radios-group"
        class="hidden-radio"
        v-model="selected"
        :options="options"
        :aria-describedby="ariaDescribedby"
        button-variant="outline-primary"
        size="md"
        name="radio-btn-outline"
        buttons
      ></b-form-radio-group>
    </b-form-group>
      </b-col>
    </b-row>
  </b-card>
</template>

<script>
import {BCard, BRow, BCol, BCardBody, BCardText, BFormGroup, BFormRadioGroup,} from 'bootstrap-vue'
export default {
    components: {
        BCard,
        BRow,
        BCol,
        BCardBody,
        BCardText,
        BFormGroup,
        BFormRadioGroup,
    },
    data() {
      return {
        selected: 'radio1',
        options: [
          { text: '38', value: '38' },
          { text: '39', value: '39' },
          { text: '40', value: '40' },
          { text: '41', value: '41' },
          { text: '42', value: '42' },
          { text: '43', value: '43' },
        ]
      }
    }
}
</script>

<style scoped>
.hidden-radio label input[type = "radio"] {
    display: none;
}
</style>