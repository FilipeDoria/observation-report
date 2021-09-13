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
        placeholder="Ship"
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
        name="especie_golginho"
        label="Espécie de Golfinho"
        :options="{
          Roaz: 'Roaz',
          Pintado: 'Pintado',
          Comum: 'Comum',
          Riscado: 'Riscado',
          Caldeirao: 'Caldeirão',
          Grampo: 'Grampo',
          Melao: 'Cabeça de melão',
          Fraser: 'Fraser',
        }"
        placeholder="Golfinho"
      />
      <FormulateInput
        type="select"
        name="especie_baleia"
        label="Espécie de Baleia"
        :options="{
          Piloto_tropical:'Piloto Tropical',
          Piloto_barbatanas:'Piloto de barbatanas Longas',
          Falsa_orca:'Falsa Orca',
        }"
        placeholder="Baleia"
      />
      <FormulateInput
        type="checkbox"
        name="misto"
        label="Avistamento Misto (2+ espécies)"
      />
      <FormulateInput
        type="number"
        name="total_individuos"
        label="Número de individuos"
        validation="required"
      />
      <FormulateInput
        type="number"
        name="crias"
        label="Número de crias"
        validation="required"
      />
      <FormulateInput
        type="select"
        name="comportamento"
        label="Comportamento"
        placeholder="Comportamento dos indivíduos"
        :options="{
          Deslocacao: 'Deslocação',
          Alimentacao: 'Alimentação',
          Repouso: 'Repouse',
          Socializacao: 'Socialização',
          Outro: 'Outro',
        }"
      />
      <FormulateInput
        type="select"
        name="reacao"
        label="Reação à embarcação"
        placeholder="Reação dos indivíduos à embarcação"
        :options="{
          Nenhuma: 'Nenhuma/Indiferença',
          Atracao: 'Atração/aproximação',
          Evitacao: 'Evitação/afastamento',
          Outro: 'Outro',
        }"
      />
      <FormulateInput
        type="select"
        name="estado_mar"
        label="Estado do mar (Beaufort)"
        validation="required"
        placeholder="0 - Calmo (< 1 Kmh)"
        :options="{
          0: '0 - Calmo (< 1 Kmh)',
          1: '1 - Aragem (1 - 5 Km/h)',
          2: '2 - Brisa Leve (6 - 11 Km/h)',
          3: '3 - Brisa Fraca (12 - 19 Km/h)',
          4: '4 - Brisa Moderada (20 - 28 Km/h)',
          5: '5 - Brisa Forte (29 - 38 Km/h)',
          6: '6 - Vento Fresco (39 - 49 Km/h)',
        }"
      />
      <FormulateInput
        type="text"
        name="observacoes"
        label="Observações importante"
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
        latitude: "",
        longitude: "",
        misto: false,
        total_individuos: "",
        crias: "",
        comportamento: "",
        reacao: "",
        estado_mar: "",
        observacoes: "",
      },
    };
  },
  methods: {
    handleSubmit() {
      //to save form items on local storage to userData variable
      localStorage.setItem('userData', JSON.stringify(this.formValues));
      console.log("Form values saved on localStorage: " + localStorage.getItem('userData'));
    },
    loadInitialData(form) {
      navigator.geolocation.getCurrentPosition(function (pos) {
        form.latitude = pos.coords.latitude.toFixed(5);
        form.longitude = pos.coords.longitude.toFixed(5);
      });

    },

  },
};



</script>