<script lang="ts">
	let questions = [
		{
			question: 'W komunikacji jesteś zwięzły/a?',
			options: [
				'Tak',
				"Od zawsze fascynowało mnie bogactwo i różnorodność języka polskiego, a szczególnie jego zdolność do tworzenia długich, złożonych wyrazów, które mogą wydawać się nieco przesadne, a wręcz niepotrzebne w codziennej komunikacji. Używanie takich słów sprawia mi ogromną przyjemność, ponieważ pozwala mi na wyrażenie myśli w sposób, który jest zarówno kreatywny, jak i nieco zabawny. W moim odczuciu, długie słowa mają w sobie pewną magię. Kiedy wypowiadam je na głos, czuję, jakby język tańczył w moich ustach, a każda sylaba dodaje nowy wymiar do mojej wypowiedzi. Na przykład, zamiast powiedzieć 'zrozumieć', mogę użyć 'przyswoić sobie złożoność zagadnienia', co nie tylko wydłuża zdanie, ale także nadaje mu pewną powagę i głębię. Często zastanawiam się, dlaczego tak bardzo pociągają mnie te nieco pretensjonalne wyrazy. Może to kwestia chęci wyróżnienia się w tłumie, pragnienia, aby moje wypowiedzi były zapamiętane i docenione. W świecie, w którym króluje szybkość i zwięzłość, ja wybieram drogę, która prowadzi przez labirynty językowych konstrukcji, gdzie każdy zakręt odkrywa nowe, nieznane dotąd słowa."
			],
			scores: ['physical', 'presentation']
		},
		{
			question: 'Czy podczas rozmowy z innymi dodajesz sumy kontrolne?',
			options: ['Tak', 'Nie', 'Integrity Check Failure'],
			scores: ['transport', 'application', 'transport']
		},
		{
			question: 'Jak się komunikujesz?',
			options: [
				'Bezpośrednio, mówię jak myślę',
				'Przed wypowiedzeniem czegoś staram się sformatować wiadomość w sposób zrozumiały dla odbiorcy.',
				'Skupiam się na podzieleniu przekazywanych informacji w zdania które mają sens.',
				'Nie zastanawiam się nad tym, ważne że rozmawiam z właściwą osobą.'
			],
			scores: ['physical', 'presentation', 'session', 'transport']
		},
		{
			question: 'Co robisz gdy napotykasz problemy?',
			options: [
				'Ignoruję je',
				'Gdy go zauważę zależnie od okoliczności dzielę się wiadomością ICMP z bliskimi',
				'Jestem bezsilny'
			],
			scores: ['application', 'network', 'physical']
		},
		{
			question: 'Strona się nie ładuje, co robisz?',
			options: [
				'Resetuję przeglądarkę',
				'Wyłączam komputer',
				'Idę dotknąć trawy (???)',
				'Usuwam ciasteczka'
			],
			scores: ['application', 'physical', 'data_link', 'session']
		},
		{
			question: 'Jaki jest twój stosunek do poczucia bezpieczeństwa?',
			options: ['Zaklejam kamerę taśmą klejącą', "Korzystam z VPN'a", 'TLS+SSL'],
			scores: ['physical', 'network', 'transport']
		},
		{
			question: 'Jak spędzasz czas wolny?',
			options: [
				'Duże grono znajomych z trwałymi znajomościami.',
				'Niezależność i ciągłą możliwość zmiany ścieżki.',
				'Ekspresję samego siebie i kreatywność.',
				'Spójność i szczerość'
			],
			scores: ['session', 'network', 'presentation', 'data_link']
		},
		{
			question: 'Jaki jest twój sposób na okazywanie wdzięczności?',
			options: [
				'KABEL SIECIOWY LAN PATCHCORD ZŁOTY MIEDŹ + SFTP CAT7 ROUTER kat 7 RJ45 10M',
				' Shrek.2.2004.PL.1080p.HD.WEBRip.1.09GiB.AAC.x264-PortalGoods ',
				"Zniżka 10% na wymianę RAM'u"
			],
			scores: ['physical', 'application', 'data_link']
		},
		{
			question: 'Kiedy zdobywasz energię?',
			options: ['Gdy ktoś podłączy wtyczkę', 'Komunikacja z najbliższymi'],
			scores: ['physical', 'session']
		},
		{
			question: 'Czego się najbardziej boisz?',
			options: ['Ryszard Masztalerz', 'Inne'],
			scores: ['network', 'application']
		},
		{
			question: 'Czym wg. Ciebie jest sukces?',
			options: [
				'200',
				'01110000011101000110111101110011011110100110010101101011001011100111000001101100',
				'nie mam pomysłu na odpowiedź :/',
				'asdhawuioawd'
			],
			scores: ['application', 'data_link', 'presentation', 'physical']
		}
	];

	let startTest = false;
	let answers = new Array(questions.length).fill(null);

	let result = '';
	let desc = 'Nieznany błąd, przepraszam :^(';

	let physical = 0;
	let data_link = 0;
	let network = 0;
	let transport = 0;
	let session = 0;
	let presentation = 0;
	let application = 0;

	function start() {
		startTest = true;
	}

	function submit() {
		// Reset all scores
		physical = data_link = network = transport = session = presentation = application = 0;

		// Calculate scores based on answers
		answers.forEach((answer, index) => {
			if (answer !== null) {
				const score = questions[index].scores[answer];
				switch (score) {
					case 'physical':
						physical++;
						break;
					case 'data_link':
						data_link++;
						break;
					case 'network':
						network++;
						break;
					case 'transport':
						transport++;
						break;
					case 'session':
						session++;
						break;
					case 'presentation':
						presentation++;
						break;
					case 'application':
						application++;
						break;
				}
			}
		});

		// Determine the highest score
		const scores = {
			'Warstwa fizyczna': physical,
			'Warstwa łącza danych': data_link,
			'Warstwa sieciowa': network,
			'Warstwa transportowa': transport,
			'Warstwa sesji': session,
			'Warstwa prezentacji': presentation,
			'Warstwa aplikacji': application
		};

		result = Object.keys(scores).reduce((a, b) => (scores[a] > scores[b] ? a : b));

		// Set description based on result
		switch (result) {
			case 'Warstwa fizyczna':
				desc = 'Jesteś osobą bardzo praktyczną i zorientowaną na konkretne działania.';
				break;
			case 'Warstwa łącza danych':
				desc = 'Masz talent do zapewniania niezawodnej komunikacji i dbasz o szczegóły.';
				break;
			case 'Warstwa sieciowa':
				desc = 'Jesteś świetnym strategiem, umiejącym łączyć różne elementy w spójną całość.';
				break;
			case 'Warstwa transportowa':
				desc = 'Twoja mocna strona to zapewnianie płynnej komunikacji i zarządzanie zasobami.';
				break;
			case 'Warstwa sesji':
				desc = 'Masz talent do nawiązywania i utrzymywania relacji, jesteś świetnym mediatorem.';
				break;
			case 'Warstwa prezentacji':
				desc = 'Jesteś kreatywną osobą z talentem do prezentowania informacji w zrozumiały sposób.';
				break;
			case 'Warstwa aplikacji':
				desc =
					'Masz zdolność do tworzenia praktycznych rozwiązań i jesteś zorientowany/a na użytkownika.';
				break;
		}
	}
</script>

<!-- O ty hakierze jeden widzę że HTML'a przeglądasz :o -->

<h1 class="py-12 text-5xl font-bold text-center text-white bg-blue-400 rounded-b-2xl">
	Test osobowości ISO/OSI
</h1>
{#if startTest}
	{#each questions as { question, options }, index}
		<div class="py-12">
			<h2 class="p-1 mb-1 text-lg">{question}</h2>
			<div class="flex flex-col space-y-2">
				{#each options as option, optionIndex}
					<label class="p-2 break-words rounded-lg bg-zinc-200">
						<input type="radio" bind:group={answers[index]} value={optionIndex} />
						{option}
					</label>
				{/each}
			</div>
		</div>
	{/each}
	<button
		on:click={submit}
		class="block mb-12 w-full h-12 text-xl font-medium text-white bg-green-500 rounded-lg md:w-72 md:mx-auto"
		>Otrzymaj wynik</button
	>
	{#if result}
		<section class="p-8 mb-12 rounded-xl bg-zinc-200">
			<h2 class="mb-8 text-2xl">Jesteś warstwą {result}!</h2>
			<p class="">{desc}</p>
		</section>
	{/if}
{:else}
	<div class="py-16 text-xl">
		<p>Miło mi Ciebie tu widzieć!</p>
		<br />
		<p>
			Chciałbym Cię zaprosić do zmuszającego do myślenia wyjątkowego doświadczenia jakim jest test
			osobowości oparty na modelu ISO/OSI dzięki któremu odkryjesz nigdy wczęściej nieznane ci
			zakamarki swojego <i><b>ja</b></i>.
		</p>
		<br />
		<p>Dziękuję za uwagę i życzę miłej podróży.</p>
	</div>
	<button
		on:click={start}
		class="block mb-12 w-full h-12 text-xl font-medium text-white bg-blue-400 rounded-lg md:w-72 md:mx-auto"
		>Rozpocznij</button
	>
{/if}

<!-- R.I.P. Stefan -->
<!-- https://www.youtube.com/watch?v=L_jWHffIx5E -->
