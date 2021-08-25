<template>
  <div>
    <h2>Ficha de registos de observações de cetáceos</h2>
    <p>Registo o máximo de informação possível.</p>
    <FormulateForm v-model="formValues" @submit="handleSubmit">
      <FormulateInput
        name="Company name"
        label="Empresa"
        validation="required"
        value="ACME"
      />
      <FormulateInput
        name="Ship name"
        label="Embarcação"
        validation="required"
        value="ship"
      />
      <FormulateInput
        type="date"
        name="Date"
        label="Data"
        validation="required"
      />
      <FormulateInput
        type="time"
        name="Time"
        label="Hora"
        validation="required"
      />
      <FormulateInput name="latitude" label="latitude" validation="required" />
      <FormulateInput
        name="longitude"
        label="longitude"
        validation="required"
      />
      <FormulateInput
        type="button"
        label="Get Location"
        @click="loadInitialData()"
      />
      <FormulateInput
        type="select"
        name="especie"
        label="Espécie"
        :options="{
          Roaz: 'Roaz',
          Pintado: 'Pintado',
          Comum: 'Comum',
        }"
        value="Roaz"
      />
      <FormulateInput
        type="checkbox"
        name="misto"
        label="Avistamento Misto (2+ espécies)"
      />
      <FormulateInput type="submit" label="Sign Up" />
    </FormulateForm>
    <h3>Values:</h3>
    {{ formValues }}
  </div>
</template>

<script>
export default {
  data: () => ({
    formValues: {},
  }),
  methods: {
    handleSubmit() {
      console.log(this.formValues);
      console.log(
        navigator.geolocation.getCurrentPosition(function (pos) {
          return pos.coords.latitude.toFixed(5);
        })
      );
    },
    loadInitialData() {
      var form = this.formValues;
      navigator.geolocation.getCurrentPosition(function (pos) {
        console.log(pos.coords.latitude.toFixed(5));
        //pos.coords.latitude.toFixed(5);
        console.log(this.latitude);
      });
      this.formValues = form;
    },
  },
};
</script>