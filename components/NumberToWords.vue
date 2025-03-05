<script>
export default {
  props: {
    number: {
      type: Number,
      required: true
    }
  },
  computed: {
    numberInWords() {
      return this.convertToWords(this.number);
    }
  },
  methods: {
    convertToWords(num) {
      const ones = ["", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine"];
      const teens = ["", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen"];
      const tens = ["", "Ten", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"];
      const thousands = ["", "Thousand", "Million", "Billion"];

      if (num === 0) return "Zero";

      function convertChunk(n) {
        let words = "";
        if (n >= 100) {
          words += ones[Math.floor(n / 100)] + " Hundred ";
          n %= 100;
        }
        if (n >= 11 && n <= 19) {
          words += teens[n - 10] + " ";
        } else {
          words += tens[Math.floor(n / 10)] + " ";
          words += ones[n % 10] + " ";
        }
        return words.trim();
      }

      let wordResult = "";
      let chunkIndex = 0;
      while (num > 0) {
        if (num % 1000 !== 0) {
          wordResult = convertChunk(num % 1000) + " " + thousands[chunkIndex] + " " + wordResult;
        }
        num = Math.floor(num / 1000);
        chunkIndex++;
      }

      return wordResult.trim();
    }
  }
};
</script>

<template>
  <span>{{ numberInWords }}</span>
</template>
