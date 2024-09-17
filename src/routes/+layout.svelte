<script>
 import "../app.css";
</script>

<head>
  <title>Test osobowości ISO/OSI</title>
</head>

<div class="flex flex-col min-h-screen">
<main class="max-w-4xl px-4 mx-auto flex-grow">
<slot />
</main>

<footer class="py-2 bg-zinc-200 border border-t border-zinc-400 mt-auto">
  <p class="text-center font-size-xl">W budowę strony pracę i <span class="text-red-500 text-2xl">&#10084</span> włożył Wojciech Woźniak</p>
</footer>
</div>
