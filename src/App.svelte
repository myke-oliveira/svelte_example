<script lang="ts">
import { onMount } from "svelte";
  let n = 5;

  $: equation = binomialEquation(n);
  $: {
    if (n < 0) {
      alert('O expoente deve ser maior ou igual a zero 0');
      n = 0;
    }
    MathJax.Hub.Typeset(document.getElementById('equation'), () => {yarn})
  }

  function binomialEquation(n: number) {
    const terms = []
    for(let k = 0; k <= n; k++) {
      const coefficient = binomialCoefficient(n, k);
      const factorX = n-k > 0 ? `x^{${n-k !== 1 ? n - k : ''}}` : ''
      const factorY = k > 0 ? `y^{${k !== 1 ? k : ''}}` : ''
      const term = `${coefficient}${factorX}${factorY}`
      terms.push(term)
    }
  
    return `$$ (x+y)^{${n}} = ${terms.join(' + ')} $$`
  }

  function binomialCoefficient(n: number, k: number) {
    return factorial(n) / (factorial(k) * factorial(n-k))
  }

  function factorial(n: number) {
    let f = 1;

    for (let i = 1; i <= n; i++)
      f *= i;

    return f
  }

  onMount(() => {
    let script = document.createElement('script');
    script.src = "https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js";
    document.head.append(script);

    script.onload = () => {
      MathJax = {
        tex: {inlineMath: [['$', '$'], ['\\(', '\\)']]},
        svg: {fontCache: 'global'}
      };
    };
  });

</script>

<main>
  <form>
    <label for="exponent">exponent</label>
    <input type="number" name="exponent" id="exponent" bind:value={n} />
  </form>
  <div id="equation">
    {@html equation}
  </div>
</main>

<style>
</style>
