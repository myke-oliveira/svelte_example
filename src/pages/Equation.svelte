<script>
  const MathJax = window.MathJax;
  export let equation;

  $: equation && MathJax.typesetPromise().then(() => {
    document.getElementById('equation').innerHTML = equation
    MathJax.typesetPromise();
  });
</script>

<div id="equation">
</div>