<script>
import { BarcodeDetectorPolyfill } from '@undecaf/barcode-detector-polyfill'

export default {
  beforeMount() {
    try {
        window['BarcodeDetector'].getSupportedFormats()
    } catch {
        window['BarcodeDetector'] = BarcodeDetectorPolyfill
    }
  },

  methods: {
    async onDetect(resultPromise) {
      this.$emit("detect", resultPromise);

      try {
        const { content } = await resultPromise;

        if (content !== null) {
          this.$emit("decode", content);
        }
      } catch (error) {
        console.error("Decoding error")
      }
    }
  }
};
</script>
