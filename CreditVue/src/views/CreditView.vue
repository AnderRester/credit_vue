<template>
  <div class="credit">
    <div id="creditApp">
      <h1>Get ready to take a credit!</h1>
      <div id="prelude">
        <input
          type="number"
          min="1"
          max="4000"
          placeholder="Money amount"
          v-model="money"
        />
        <input
          type="number"
          min="0"
          max="100"
          placeholder="Percent"
          v-model="percent"
        />
        <select name="" id="" v-model="time">
          <option value="undefined" disabled>Select Period</option>
          <option value="1">1 Month</option>
          <option value="2">2 Months</option>
          <option value="3">3 Months</option>
          <option value="4">4 Months</option>
          <option value="5">5 Months</option>
          <option value="6">6 Months</option>
          <option value="7">7 Months</option>
          <option value="8">8 Months</option>
          <option value="9">9 Months</option>
          <option value="10">10 Months</option>
          <option value="11">11 Months</option>
          <option value="12">12 Months</option>
        </select>
        <button id="calculate" @click="printCreditTable()">Calculate</button>
      </div>
      <div id="printTable">
        <div id="attributes">
          <div id="id">
            <div>Month</div>
          </div>
          <div id="time">
            <div>Period</div>
          </div>
          <div id="percent">
            <div>Percent</div>
          </div>
          <div id="rest">
            <div>Rest</div>
          </div>
          <div id="toPay">
            <div>to Pay</div>
          </div>
        </div>
        <div id="dataBaseData">
          <div id="id_dataBase"></div>
          <div id="time_dataBase"></div>
          <div id="percent_dataBase"></div>
          <div id="rest_dataBase"></div>
          <div id="toPay_dataBase"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { createElementBlock } from "@vue/runtime-core";
export default {
  data() {
    return {
      dataBase: [],
      time: undefined,
      money: 0,
      percent: 0,
      rest: 0,
      toPay: 0,
      id: 0,
      timeTemp: this.time,
    };
  },
  computed: {},
  methods: {
    getRest() {
      if (this.percent == 0) {
        if (this.money % this.time == 0) {
          return this.money / this.time;
        } else {
          return parseInt(this.money / this.time);
        }
      }
    },
    printCreditTable() {
      //   const id = document.getElementById("id");
      //   const time = document.getElementById("time");
      //   const percent = document.getElementById("percent");
      //   const rest = document.getElementById("rest");

      let id_dataBase = document.getElementById("id_dataBase");
      let time_dataBase = document.getElementById("time_dataBase");
      let percent_dataBase = document.getElementById("percent_dataBase");
      let rest_dataBase = document.getElementById("rest_dataBase");
      let toPay_dataBase = document.getElementById("toPay_dataBase");
      this.dataBase = [];
      id_dataBase.innerHTML = "";
      time_dataBase.innerHTML = "";
      percent_dataBase.innerHTML = "";
      rest_dataBase.innerHTML = "";
      toPay_dataBase.innerHTML = "";
      //   this.time = this.timeTemp;
      this.id = 0;
      //   this.time = 0;
      this.toPay = this.money;
      let periodTemp = this.time;
      periodTemp++;
      for (let i = 0; i < this.time; i++) {
        this.id++;
        periodTemp--;
        // this.time--;
        this.dataBase.push({
          id: this.id,
          time: this.time,
          percent: this.percent,
          rest: this.getRest(),
          toPay: this.toPay,
        });
        console.log(this.dataBase);
        id_dataBase.append(this.dataBase[i].id, document.createElement("br"));
        time_dataBase.append(periodTemp, document.createElement("br"));
        percent_dataBase.append(
          this.dataBase[i].percent,
          document.createElement("br")
        );
        if (i == this.time - 1) {
          rest_dataBase.append(
            (this.dataBase[i].rest = (
              this.getRest() +
              (this.money / this.time - this.getRest()) * this.time
            ).toFixed(2)),
            document.createElement("br")
          );
        } else {
          rest_dataBase.append(
            (this.dataBase[i].rest = this.getRest().toFixed(2)),
            document.createElement("br")
          );
        }
        toPay_dataBase.append(
          (this.toPay -= this.dataBase[i].rest),
          document.createElement("br")
        );
      }
    },
  },
};
</script>


<style>
@media (width: 1024px) {
  .credit {
    display: flex;
    align-items: center;
  }
}
#printTable {
  display: grid;
  background: rgb(87, 87, 87);
}
#attributes,
#dataBaseData {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
}
#id,
#time,
#percent,
#rest,
#toPay,
#id_dataBase,
#time_dataBase,
#percent_dataBase,
#rest_dataBase,
#toPay_dataBase {
  border-right: 1px solid #000;
  border-bottom: 1px solid #000;
  padding: 8px;
}
</style>
