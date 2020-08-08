<template>
  <v-row justify="center">
    <v-col cols="12" sm="7" md="6">
      <v-form>
        <v-textarea
          v-model="dataset"
          auto-grow
          hint="Numbers to be separated with commas"
          outlined
          placeholder="Paste your data here"
        ></v-textarea>
        <v-btn color="primary" block large>Plot a graph</v-btn>
      </v-form>
      <v-simple-table fixed-header>
        <template v-slot:default>
          <thead>
            <tr>
              <th>d</th>
              <th>Current (%)</th>
              <th>Expected (%)</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>1</td>
              <td>{{ firstDigitFrequency.one }}</td>
              <td>{{ frequencyDistribution(1) }}</td>
            </tr>
            <tr>
              <td>2</td>
              <td>{{ firstDigitFrequency.two }}</td>
              <td>{{ frequencyDistribution(2) }}</td>
            </tr>
            <tr>
              <td>3</td>
              <td>{{ firstDigitFrequency.three }}</td>
              <td>{{ frequencyDistribution(3) }}</td>
            </tr>
            <tr>
              <td>4</td>
              <td>{{ firstDigitFrequency.four }}</td>
              <td>{{ frequencyDistribution(4) }}</td>
            </tr>
            <tr>
              <td>5</td>
              <td>{{ firstDigitFrequency.five }}</td>
              <td>{{ frequencyDistribution(5) }}</td>
            </tr>
            <tr>
              <td>6</td>
              <td>{{ firstDigitFrequency.six }}</td>
              <td>{{ frequencyDistribution(6) }}</td>
            </tr>
            <tr>
              <td>7</td>
              <td>{{ firstDigitFrequency.seven }}</td>
              <td>{{ frequencyDistribution(7) }}</td>
            </tr>
            <tr>
              <td>8</td>
              <td>{{ firstDigitFrequency.eight }}</td>
              <td>{{ frequencyDistribution(8) }}</td>
            </tr>
            <tr>
              <td>9</td>
              <td>{{ firstDigitFrequency.nine }}</td>
              <td>{{ frequencyDistribution(9) }}</td>
            </tr>
          </tbody>
        </template>
      </v-simple-table>
    </v-col>
  </v-row>
</template>
<script>
export default {
  data() {
    return {
      dataset: '',
    }
  },
  computed: {
    dataAsArray() {
      const dtArray = this.dataset.split(',')
      const onlyNumbers = dtArray.map((dt) => {
        if (!isNaN(dt)) {
          return parseFloat(dt)
        }
      })
      return onlyNumbers.filter((nb) => {
        return !isNaN(nb)
      })
    },
    firstDigitFrequency() {
      let one = 0
      let two = 0
      let three = 0
      let four = 0
      let five = 0
      let six = 0
      let seven = 0
      let eight = 0
      let nine = 0
      this.dataAsArray.forEach((dt) => {
        const leadingDigit = parseInt(dt.toString().split('')[0])
        switch (leadingDigit) {
          case 1:
            one++
            break
          case 2:
            two++
            break
          case 3:
            three++
            break
          case 4:
            four++
            break
          case 5:
            five++
            break
          case 6:
            six++
            break
          case 7:
            seven++
            break
          case 8:
            eight++
            break
          case 9:
            nine++
            break
          default:
            break
        }
      })
      const total = one + two + three + four + five + six + seven + eight + nine
      if (total === 0) {
        return {
          one,
          two,
          three,
          four,
          five,
          six,
          seven,
          eight,
          nine,
        }
      }
      return {
        one: ((100 * one) / total).toFixed(2),
        two: ((100 * two) / total).toFixed(2),
        three: ((100 * three) / total).toFixed(2),
        four: ((100 * four) / total).toFixed(2),
        five: ((100 * five) / total).toFixed(2),
        six: ((100 * six) / total).toFixed(2),
        seven: ((100 * seven) / total).toFixed(),
        eight: ((100 * eight) / total).toFixed(2),
        nine: ((100 * nine) / total).toFixed(2),
      }
    },
  },
  methods: {
    frequencyDistribution(digit = 0) {
      const step1 = Math.pow(digit, -1)
      const step2 = step1 + 1
      const step3 = Math.log10(step2) * 100
      return step3.toFixed(2)
    },
  },
}
</script>
