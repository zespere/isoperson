<script lang="ts">
  let questions = [
    {
      question: "Czy podczas rozmowy z innymi dodajesz sumy kontrolne?",
      options: ["Tak", "Nie", "Integrity Check Failure"]
    },
    {
      question: "Jak się komunikujesz?",
      options: ["Bezpośrednio, mówię jak myślę", "Przed wypowiedzeniem czegoś staram się sformatować wiadomość w sposób zrozumiały dla odbiorcy.", "Skupiam się na podzieleniu przekazywanych informacji w zdania które mają sens.", "Nie zastanawiam się nad tym, ważne że rozmawiam z właściwą osobą."]
    },
    {
      question: "Informacje przekazujesz prosto i klarownie czy lubisz urozmaicać rozmowy wymianę danych metaforami?",
      options: ["Jestem bezpośredni(a)", "Lubię metafory i kwiecisty język", "Ludzki umysł jak i język jest nieprecyzyjny a więc w pełni wydajna komunikacja jest niemożliwa."]
    },
    {
      question: "Co robisz gdy napotykasz problemy?",
      options: ["Ignoruję je", "Gdy go zauważę zależnie od okoliczności dzielę się wiadomością ICMP z bliskimi", "Jestem bezsilny"]
    },
    {
      question: "Jaki jest twój stosunek do poczucia bezpieczeństwa?",
      options: ["Ignoruję je", "Gdy go zauważę zależnie od okoliczności dzielę się wiadomością ICMP z bliskimi", "Jestem bezsilny"]
    },
    {
      question: "Jak wyglądają twoje relacje społeczne?",
      options: ["Lubię zakładać nowe znajomości i je kultywować"]
    },
    {
      question: "Jaki jest twój stosunek do poczucia bezpieczeństwa?",
      options: ["Ignoruję je", "Gdy go zauważę zależnie od okoliczności dzielę się wiadomością ICMP z bliskimi", "Jestem bezsilny"]
    },
    {
      question: "",
      options: ["Duże grono znajomych z trwałymi znajomościami.", "Niezależność i ciągłą możliwość zmiany ścieżki.", "Ekspresję samego siebie i kreatywność.", "Spójność i szczerość"]
    },
    {
      question: "Co uważasz za najważniejsze.",
      options: ["Duże grono znajomych z trwałymi znajomościami.", "Niezależność i ciągłą możliwość zmiany ścieżki.", "Ekspresję samego siebie i kreatywność.", "Spójność i szczerość"]
    },
    {
      question: "Co uważasz za najważniejsze.",
      options: ["Duże grono znajomych z trwałymi znajomościami.", "Niezależność i ciągłą możliwość zmiany ścieżki.", "Ekspresję samego siebie i kreatywność.", "Spójność i szczerość"]
    },
    {
      question: "Co uważasz za najważniejsze.",
      options: ["Duże grono znajomych z trwałymi znajomościami.", "Niezależność i ciągłą możliwość zmiany ścieżki.", "Ekspresję samego siebie i kreatywność.", "Spójność i szczerość"]
    },
    {
      question: "Co uważasz za najważniejsze.",
      options: ["Duże grono znajomych z trwałymi znajomościami.", "Niezależność i ciągłą możliwość zmiany ścieżki.", "Ekspresję samego siebie i kreatywność.", "Spójność i szczerość"]
    },
    {
      question: "Co uważasz za najważniejsze.",
      options: ["Duże grono znajomych z trwałymi znajomościami.", "Niezależność i ciągłą możliwość zmiany ścieżki.", "Ekspresję samego siebie i kreatywność.", "Spójność i szczerość"]
    }
  ];

  let answers = Array(questions.length).fill(null);
  let result = "";
  let desc = "Nieznany błąd, przepraszam :^(";
  let physical = 0;
  let data_link = 0;
  let network = 0;
  let transport = 0;
  let session = 0;
  let presentation = 0;
  let application = 0;

  function submit() {
    const score = answers.reduce((acc, answer) => acc + (answer ? answer : 0), 0);
    if (score < 3) {
      result = "You are an introvert!";
    } else if (score < 6) {
      result = "You are an ambivert!";
    } else {
      result = "You are an extrovert!";
    }
  }
</script>

<div>
  <h1 class="bg-blue-400 text-5xl text-white font-bold text-center py-12 rounded-b-2xl">Test osobowości ISO/OSI</h1>
  <div class="py-16 text-xl">
  <p> Miło mi Ciebie tu widzieć! </p> <br />
  <p> Chciałbym Cię zaprosić do zmuszającego do myślenia wyjątkowego doświadczenia jakim jest test osobowości oparty na modelu ISO/OSI dzięki któremu odkryjesz nigdy wczęściej nieznane ci zakamarki swojej osobowości. </p> <br/>
  <p> Dziękuję za uwagę i życzę miłej podróży. </p>
  </div>
  {#each questions as { question, options }, index}
    <div class="py-12">
      <h2>{question}</h2>
      <div class="flex flex-col space-y-2">
        {#each options as option, optionIndex}
          <label class="p-2 bg-zinc-200 rounded-lg">
            <input type="radio" bind:group={answers[index]} value={optionIndex} />
            {option}
          </label>
        {/each}
      </div>
    </div>
  {/each}
  <button on:click={submit} class="bg-green-500 w-72 h-12 rounded-lg text-white text-xl font-medium text-center">Otrzymaj wynik</button>
  {#if result}
    <section class="p-8 bg-zinc-200 rounded-xl my-12">
    <h2 class="text-2xl mb-8">Jesteś {result}!</h2>
    <p class="">{desc}</p>
    </section>
  {/if}
</div>
