<script lang="ts">
  import "./app.css";
  import { Router, Link, Route } from "svelte-routing";
  import BinomialFormula from "./pages/BinomialFormula.svelte";
  // import ComplexNumbers from "./pages/ComplexNumbers.svelte";

  export let url = ""
</script>

<Router { url }>
  <nav>
    <Link to="/binomial-formula">Fórmula Binomial</Link>
    <!-- <Link to="/complex-numbers">Números Complexos</Link> -->
  </nav>
  <main>
    <Route path="/binomial-formula" component={ BinomialFormula } />
    <!-- <Route path="/complex-numbers" component={ ComplexNumbers } /> -->
  </main>
</Router>

<style>
  nav {
    display: flex;
    gap: 2rem;
    padding: 2rem;
  }

  main {
    margin-top: 4rem;
    text-align: center;
  }
</style>
