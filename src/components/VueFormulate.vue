<template>
  <div>
    <h2>Ficha de registos de observações de cetáceos</h2>
    <p>Registe o máximo de informação possível.</p>
    <FormulateForm v-model="formValues" @submit="handleSubmit">
      <FormulateInput
        name="company"
        label="Empresa"
        validation="required"
        placeholder="ACME"
      />
      <FormulateInput
        name="ship"
        label="Embarcação"
        validation="required"
        placeholder="ship"
      />
      <FormulateInput
        type="date"
        name="date"
        label="Data"
        validation="required"
      />
      <FormulateInput
        type="time"
        name="time"
        label="Hora"
        validation="required"
      />
      <FormulateInput name="latitude" label="Latitude" validation="required" />
      <FormulateInput
        name="longitude"
        label="Longitude"
        validation="required"
      />
      <FormulateInput
        type="button"
        label="Obter posição"
        @click="loadInitialData(formValues)"
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
        placeholder="Roaz"
      />
      <FormulateInput
        type="checkbox"
        name="misto"
        label="Avistamento Misto (2+ espécies)"
      />
      <FormulateInput type="submit" label="Enviar" />
    </FormulateForm>
    <h3>Values:</h3>
    {{ formValues }}
  </div>
</template>

<script>
export default {
  data() {
    return {
      formValues : {
        company: "",
        ship: "",
        especie: "",
        date: "",
        time: "",
        latitude: "0",
        longitude: "0",
        misto: false,
      },
    };
  },
  methods: {
    handleSubmit() {
      
      //to save form items on local storage to userData variable
      localStorage.setItem('userData', JSON.stringify(this.formValues));
      console.log(localStorage.getItem('userData'));

      console.log(this.formValues);
      console.log(
        navigator.geolocation.getCurrentPosition(function (pos) {
          return pos.coords.latitude.toFixed(5);
        })
      );
    },
    loadInitialData(form) {
      navigator.geolocation.getCurrentPosition(function (pos) {
        form.latitude = pos.coords.latitude.toFixed(5);
        form.longitude = pos.coords.longitude.toFixed(5);
        console.log(form.latitude);
      });

    },

  },
};



</script>