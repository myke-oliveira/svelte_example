<script lang="ts">
  import Equation from "./Equation.svelte";

  let n = 2;
  $: equation = binomialEquation(n);
  $: {
    if (n < 0) {
      alert('O expoente deve ser maior ou igual a zero 0.');
      n = 0;
    }
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
  
    return `$$ (x+y)^{${n}} = ${terms.join(' + ')} $$`;
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

</script>

<main>
  <h1>Expoente: </h1>
  <form>
    <input type="number" name="exponent" id="exponent" bind:value={n}/>
  </form>
  <Equation {equation}/>  
</main>

<style>
</style>
