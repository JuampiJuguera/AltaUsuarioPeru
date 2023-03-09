<template>
  <div class="info-box-content">
    <p>
      Maqueta Alta de usuario Peru - por favor revisar que los datos sean
      correctos - La subida de archivos es simbolica no funciona - en los
      selectores no toda la informacion fue cargada, por ejemplo en ciudades
      solo pusimos Lima y San Martin
    </p>
    <el-steps
      :active="step"
      finish-status="success"
      align-center
      style="margintop: 50px"
    >
      <el-step title="Datos Generales"></el-step>
      <el-step title="Formas de pago / Datos Bancarios"></el-step>
      <el-step title="Identificación de la Empresa"></el-step>
      <el-step title="Usuario" v-if="!provider"></el-step>
    </el-steps>
    <div>
      <p class="text-danger" style="margintop: 50px">
        Los campos acompañados con asterisco(*) son obligatorios.
      </p>
    </div>
    <el-divider>Datos de la empresa</el-divider>
    <el-form class="rucForm" style="margintop: 50px" v-if="step == 0">
      <el-form-item label="RUC (sin guiones)">
        <el-row>
          <el-col :span="6" style="padding-right: 20px; width: 900px">
            <el-input
              id="RUC"
              v-model.number="ruc"
              type="text"
              maxlength="11"
              show-word-limit
            ></el-input>
          </el-col>
          <el-col :span="2">
            <el-button
              id="verificarRUC"
              size="mini"
              type="primary"
              v-on:click="validateRuc = true"
            >
              Verificar RUC
            </el-button>
          </el-col>
          <el-col :span="7">
            se verifica el RUC aparecen los datos generales
          </el-col>
        </el-row>
      </el-form-item>
    </el-form>
    <el-form id="step1" v-if="validateRuc && step == 0" label-position="top">
      <div style="margintop: 50px; marginbottom: 10px">
        Step 1 - Datos generales
      </div>

      <el-form-item>
        <el-col :span="6">
          <el-form-item label="Razón Social*">
            <el-input v-model="generalData.company" />
          </el-form-item>
        </el-col>
      </el-form-item>

      <el-form-item>
        <el-col :span="6">
          <el-form-item label="Nombre comercial">
            <el-input v-model="generalData.companyName" />
          </el-form-item>
        </el-col>
      </el-form-item>
      <el-form-item>
        <el-row>
          <el-form-item label="Pais*">
            <el-select
              placeholder="Selecciona Pais"
              v-model="generalData.country"
            >
              <el-option label="Peru" value="Peru" />
            </el-select>
          </el-form-item>
        </el-row>
      </el-form-item>
      <el-form-item>
        <el-row>
          <el-form-item label="Ciudad*">
            <el-select
              placeholder="Selecciona ciudad"
              v-model="generalData.city"
            >
              <el-option label="Lima" value="Lima" />
              <el-option label="San Martin" value="San Martin" />
            </el-select>
          </el-form-item>
        </el-row>
      </el-form-item>
      <el-form-item>
        <el-col :span="6">
          <el-form-item label="Localidad*">
            <el-input v-model="generalData.locality" />
          </el-form-item>
        </el-col>
      </el-form-item>
      <el-form-item>
        <el-col :span="6">
          <el-form-item label="Dirección*">
            <el-input v-model.number="generalData.address" />
          </el-form-item>
        </el-col>
      </el-form-item>
      <el-form-item>
        <el-col :span="6">
          <el-form-item label="Código Postal*">
            <el-input v-model.number="generalData.zip" />
          </el-form-item>
        </el-col>
      </el-form-item>
      <el-form-item>
        <el-col :span="6">
          <el-form-item label="Telefono*">
            <el-input v-model.number="generalData.phone" />
          </el-form-item>
        </el-col>
      </el-form-item>
      <el-form-item>
        <el-col :span="6">
          <el-form-item label="Email*">
            <el-input v-model="generalData.email" />
          </el-form-item>
        </el-col>
      </el-form-item>
      <el-row>
        <el-col :span="4" style="marginbottom: 25px">
          <p style="font-size: 14px">
            Constancia de inscripcion RUC - Ficha RUC
          </p>
          <el-upload v-model="generalData.rucDataSheet">
            <el-button type="primary">select file</el-button>
          </el-upload>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="4">
          <p style="font-size: 14px">Constancia de Registro de Tributos</p>
          <el-upload v-model="generalData.rucDataSheet">
            <el-button type="primary">select file</el-button>
          </el-upload>
        </el-col>
      </el-row>
      <el-button size="mini" type="primary" @click="next">
        Siguiente Paso
      </el-button>
    </el-form>
    <el-form v-if="step == 1" label-position="top">
      <div style="margintop: 50px; marginbottom: 50px">
        Step 2 - Formas de pago/Datos Bancarios
      </div>
      Cuenta 1
      <el-form-item>
        <el-row>
          <el-form-item label="Banco*">
            <el-select
              placeholder="Selecciona Banco"
              v-model="paymentData.firstBank"
            >
              <el-option
                label="Banco de credito del Peru"
                value="Banco de credito del Peru"
              />
            </el-select>
          </el-form-item>
        </el-row>
      </el-form-item>
      <el-form-item>
        <el-col :span="6">
          <el-form-item label="Nro Cuenta 1*">
            <el-input v-model.number="paymentData.firstAccountNumber" />
          </el-form-item>
        </el-col>
      </el-form-item>
      <el-form-item>
        <el-row>
          <el-form-item label="Tipo*">
            <el-select
              placeholder="Selecciona Tipo"
              v-model="paymentData.firstType"
            >
              <el-option label="Cuenta Corriente" value="Cuenta Corriente" />
            </el-select>
          </el-form-item>
        </el-row>
      </el-form-item>
      <el-form-item>
        <el-row>
          <el-form-item label="Moneda*">
            <el-select
              placeholder="Selecciona la moneda"
              v-model="paymentData.firstCurrency"
            >
              <el-option label="Soles" value="Soles" />
              <el-option label="Dolares" value="Dolares" />
            </el-select>
          </el-form-item>
        </el-row>
      </el-form-item>
      <el-form-item>
        <el-col :span="6">
          <el-form-item label="Nro CCI*">
            <el-input v-model.number="paymentData.firstCCI" />
          </el-form-item>
        </el-col>
      </el-form-item>
      Cuenta 2
      <el-form-item>
        <el-row>
          <el-form-item label="Banco*">
            <el-select
              placeholder="Selecciona Banco"
              v-model="paymentData.secondBank"
            >
              <el-option
                label="Banco de credito del Peru"
                value="Banco de credito del Peru"
              />
            </el-select>
          </el-form-item>
        </el-row>
      </el-form-item>
      <el-form-item>
        <el-col :span="6">
          <el-form-item label="Nro Cuenta 2*">
            <el-input v-model.number="paymentData.secondAccountNumber" />
          </el-form-item>
        </el-col>
      </el-form-item>
      <el-form-item>
        <el-row>
          <el-form-item label="Tipo*">
            <el-select
              placeholder="Selecciona Tipo"
              v-model="paymentData.secondType"
            >
              <el-option label="Cuenta Corriente" value="Cuenta Corriente" />
            </el-select>
          </el-form-item>
        </el-row>
      </el-form-item>
      <el-form-item>
        <el-row>
          <el-form-item label="Moneda*">
            <el-select
              placeholder="Selecciona la moneda"
              v-model="paymentData.secondCurrency"
            >
              <el-option label="Soles" value="Soles" />
              <el-option label="Dolares" value="Dolares" />
            </el-select>
          </el-form-item>
        </el-row>
      </el-form-item>
      <el-form-item>
        <el-col :span="6">
          <el-form-item label="Nro CCI*">
            <el-input v-model.number="paymentData.secondCCI" />
          </el-form-item>
        </el-col>
      </el-form-item>
      <el-row>
        <el-col :span="4" style="marginbottom: 25px">
          <p style="font-size: 14px">
            Instrucciones para acreditación de pagos
          </p>
          <el-upload v-model="generalData.rucDataSheet">
            <el-button type="primary">select file</el-button>
          </el-upload>
        </el-col>
      </el-row>
      <el-button size="mini" type="primary" @click="next">
        Siguiente Paso
      </el-button>
    </el-form>
    <el-form label-position="top" v-if="step == 2">
      <div style="margintop: 50px; marginbottom: 50px">
        Step 3 - Identificación de la Empresa
      </div>
      <el-form-item>
        <el-col :span="6">
          <el-form-item label="Partida Registral*">
            <el-input v-model.number="companyData.registryEntry" />
          </el-form-item>
        </el-col>
      </el-form-item>
      <el-form-item>
        <el-row>
          <el-form-item label="Régimen Tributario*">
            <el-select
              placeholder="Selecciona el regimen"
              v-model.number="companyData.taxRegimen"
            >
              <el-option
                label="REGIMEN MYPE TRIBUTARIO"
                value="REGIMEN MYPE TRIBUTARIO"
              />
            </el-select>
          </el-form-item>
        </el-row>
      </el-form-item>
      <el-form-item>
        <el-row>
          <el-form-item label="Tipo de comprobantes a emitir*">
            <el-select
              placeholder="Selecciona el tipo"
              v-model.number="companyData.type"
            >
              <el-option
                label="Facturas Electronicas"
                value="Facturas Electronicas"
              />
            </el-select>
          </el-form-item>
        </el-row>
      </el-form-item>
      <el-row>
        <p style="textalign: left">
          Su empresa es agente de retecion y/o percepción?
        </p>
      </el-row>
      <el-form-item>
        <el-switch
          size="large"
          style="
            --el-switch-on-color: #13ce66;
            --el-switch-off-color: #ff4949;
            margin-left: 25px;
          "
          active-text="Si"
          inactive-text="No"
          v-model="companyData.agent"
        />
      </el-form-item>
      <el-form-item label="Detallar" style="margin-left: 25px">
        <el-input v-model="companyData.details" style="width: 500px" />
      </el-form-item>
      <el-row>
        <p style="textalign: left">
          Su empresa realiza operaciones sujetas a detracción?
        </p>
      </el-row>
      <el-form-item>
        <el-row :gutter="20" style="margin-bottom: 20px">
          <el-switch
            size="large"
            style="
              --el-switch-on-color: #13ce66;
              --el-switch-off-color: #ff4949;
              margin-left: 35px;
            "
            active-text="Si"
            inactive-text="No"
            v-model="companyData.detractionsCompany"
          />
        </el-row>
      </el-form-item>
      <el-row style="margin-left: 25px">
        <el-form-item label="Tasa %" v-if="companyData.detractionsCompany">
          <el-input type="number" v-model="companyData.rate" />
        </el-form-item>
        <el-form-item
          label="Codigo ope.:"
          v-if="companyData.detractionsCompany"
        >
          <el-input v-model="companyData.code" />
        </el-form-item>
      </el-row>
      <el-col :span="6" style="margin-left: 25px">
        <el-form-item
          label="Número de cuenta de detracciones Banco de la Nación"
          v-if="companyData.detractionsCompany"
        >
          <el-input v-model="companyData.detractionsNumber" />
        </el-form-item>
      </el-col>
      <el-row v-if="companyData.detractionsCompany">
        <el-col :span="4">
          <p style="font-size: 14px">Instrucciones Cuenta detracciones</p>
          <el-upload v-model="generalData.rucDataSheet">
            <el-button type="primary">select file</el-button>
          </el-upload>
        </el-col>
      </el-row>
      <el-button size="mini" type="primary" @click="next">
        Siguiente Paso
      </el-button>
    </el-form>
    <el-form v-if="step == 3" label-position="top">
      <div style="margintop: 50px; marginbottom: 50px">Step 4 - Usuario</div>
      <el-form-item>
        <el-col :span="10">
          <el-form-item label="Usuario*">
            <el-input v-model="userData.userName" />
          </el-form-item>
        </el-col>
      </el-form-item>
      <el-form-item>
        <el-col :span="10">
          <el-form-item label="Email">
            <el-input v-model="userData.email" />
          </el-form-item>
        </el-col>
      </el-form-item>
      <el-form-item>
        <el-col :span="10">
          <el-form-item label="Contraseña">
            <el-input type="password" v-model="userData.password" />
          </el-form-item>
        </el-col>
      </el-form-item>
      <el-form-item>
        <el-col :span="10">
          <el-form-item label="Repetir Contraseña">
            <el-input type="password" v-model="userData.repeatpw" />
          </el-form-item>
        </el-col>
      </el-form-item>
      <el-button size="mini" type="primary" @click="next">
        Volver al principio
      </el-button>
    </el-form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      ruc: "",
      step: 0,
      validateRuc: false,
      generalData: {
        company: "",
        companyName: "",
        country: "",
        city: "",
        locality: "",
        address: "",
        zip: "",
        phone: "",
        email: "",
        rucDataSheet: "",
        taxRegistrationProof: "",
      },
      paymentData: {
        firstBank: "",
        firstAccountNumber: "",
        firstType: "",
        firstCurrency: "",
        firstCCI: "",
        secondBank: "",
        secondAccountNumber: "",
        secondType: "",
        secondCurrency: "",
        secondCCI: "",
      },
      companyData: {
        registryEntry: "",
        taxRegimen: "",
        type: "",
        agent: true,
        details: "",
        detractionsCompany: true,
        rate: 0,
        code: "",
        detractionsNumber: "",
      },
      userData: {
        userName: "",
        email: "",
        password: "",
        repeatpw: "",
      },
    };
  },
  methods: {
    next() {
      console.log(this.step);
      if (this.step++ >= 3) {
        this.step = 0;
        this.validateRuc = false;
      }
    },
  },
};
</script>

<style>
body {
  background-color: #ecf0f5;
}

el-input {
  width: 400px;
}
</style>
