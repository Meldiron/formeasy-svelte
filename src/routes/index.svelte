<script lang="ts">
	let googleScriptUrl =
		'https://script.google.com/macros/s/AKfycbxq6AVAIabOoux0I9GjpchAiL0IjqcKgmijUvQomfhwBkxMJtR65mbjKRjib3Hqp6Zj/exec';

	let googleSheetUrl =
		'https://docs.google.com/spreadsheets/d/1EboWQU3S86CCUqwi7oVIdSsLoErJhDVolSbzHsUadIQ/edit?usp=sharing';

	let name = '';
	let email = '';
	let company = '';
	let country = '';
	let message = '';

	let loading = false;
	let responseMessage = '';

	async function submitForm() {
		if (loading) {
			return;
		}

		const data = {
			name,
			email,
			company,
			country,
			message
		};

		loading = true;

		try {
			const response = await fetch(googleScriptUrl, {
				method: 'POST',
				headers: {
					'Content-Type': 'text/plain;charset=utf-8'
				},
				body: JSON.stringify(data)
			});

			const json = await response.json();
			responseMessage = json.message;

			name = '';
			email = '';
			company = '';
			country = '';
			message = '';
		} catch (err: any) {
			responseMessage = err.message ?? err;
		} finally {
			loading = false;
		}
	}
</script>

<div class="bg-gradient-to-b from-slate-900 to-black w-full pb-16">
	<div class="md:px-20 px-4 py-8">
		<div
			class="flex flex-col space-y-6 md:space-y-0 md:flex-row md:space-x-3 items-center  justify-between"
		>
			<div class="text-white font-bold text-2xl">
				FormEasy <span class="font-normal">| Svelte Demo</span>
			</div>
			<a
				href="https://github.com/Meldiron/formeasy-svelte/"
				class="flex items-center justify-center space-x-3 text-base font-medium leading-none text-[#181717] py-4 px-5 bg-white rounded focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-slate-500 hover:bg-gray-200"
			>
				<svg
					class="w-6 text-[#181717]"
					role="img"
					viewBox="0 0 24 24"
					xmlns="http://www.w3.org/2000/svg"
					><title>GitHub</title><path
						d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"
					/></svg
				>
				<span class="shrink-0">Visit on GitHub</span>
			</a>
		</div>
	</div>

	<div class="flex flex-col items-center justify-center pb-8">
		<p class="uppercase font-light text-lg mb-2 text-white">Made using</p>
		<a href="https://github.com/Basharath/FormEasy">
			<img src="/formeasy-logo.svg" class="h-10" alt="FormEasy logo" />
		</a>
	</div>
</div>

<div class="w-full flex items-center justify-center mb-12 -mt-16">
	<form
		on:submit|preventDefault={submitForm}
		class="mx-auto max-w-[900px] bg-white shadow rounded py-12 lg:px-28 px-8"
	>
		<p class="md:text-3xl text-xl font-bold leading-7 text-center text-gray-700 ">
			Let's Make a Contact Form
		</p>
		<div class="md:flex items-center mt-12">
			<div class="md:w-72 flex flex-col">
				<label for="name" class="text-base font-semibold leading-none text-gray-800 ">Name</label>
				<input
					bind:value={name}
					id="name"
					tabindex="0"
					arial-label="Please input name"
					type="text"
					class="text-base leading-none text-gray-900 p-3 focus:oultine-none focus:border-indigo-700 mt-4 bg-gray-100 border rounded border-gray-200 placeholder-gray-100"
					placeholder="Please input name"
				/>
			</div>
			<div class="md:w-72 flex flex-col md:ml-6 md:mt-0 mt-4">
				<label for="email" class="text-base font-semibold leading-none text-gray-800 "
					>Email Address</label
				>
				<input
					bind:value={email}
					id="email"
					tabindex="0"
					arial-label="Please input email address"
					type="email"
					class="text-base leading-none text-gray-900 p-3 focus:oultine-none focus:border-indigo-700 mt-4 bg-gray-100 border rounded border-gray-200 placeholder-gray-100"
					placeholder="Please input email address"
				/>
			</div>
		</div>
		<div class="md:flex items-center mt-8">
			<div class="md:w-72 flex flex-col">
				<label for="company" class="text-base font-semibold leading-none text-gray-800 "
					>Company name</label
				>
				<input
					bind:value={company}
					id="company"
					tabindex="0"
					arial-label="Please input company name"
					type="text"
					class="text-base leading-none text-gray-900 p-3 focus:oultine-none focus:border-indigo-700 mt-4 bg-gray-100 border rounded border-gray-200 placeholder-gray-100"
					placeholder="Please input company name"
				/>
			</div>
			<div class="md:w-72 flex flex-col md:ml-6 md:mt-0 mt-4">
				<label for="country" class="text-base font-semibold leading-none text-gray-800 "
					>Country</label
				>
				<input
					bind:value={country}
					id="country"
					tabindex="0"
					arial-label="Please input country name"
					type="text"
					class="text-base leading-none text-gray-900 p-3 focus:oultine-none focus:border-indigo-700 mt-4 bg-gray-100 border rounded border-gray-200 placeholder-gray-100"
					placeholder="Please input country name"
				/>
			</div>
		</div>
		<div>
			<div class="w-full flex flex-col mt-8">
				<label for="message" class="text-base font-semibold leading-none text-gray-800 "
					>Message</label
				>
				<textarea
					bind:value={message}
					required={true}
					tabindex="0"
					aria-label="leave a message"
					type="text"
					id="message"
					class="h-36 text-base leading-none text-gray-900 p-3 focus:oultine-none focus:border-indigo-700 mt-4 bg-gray-100 border rounded border-gray-200 placeholder-gray-100 resize-none"
				/>
			</div>
		</div>
		<p class="text-xs leading-3 text-gray-600  mt-4">
			<span class="text-red-500 font-bold">Anything you put here is public!</span> Don't put your personal
			data in the form please. Just use something fake, thanks!
		</p>
		<div
			class="mt-9  flex flex-col space-y-3 md:flex-row md:space-y-0 md:space-x-3 items-center justify-center w-full"
		>
			<button
				type="submit"
				class="w-full md:w-[fit-content] flex items-center justify-center space-x-3 text-base font-semibold leading-none text-white py-4 px-10 bg-slate-700 rounded hover:bg-slate-600 focus:ring-2 focus:ring-offset-2 focus:ring-slate-700 focus:outline-none"
			>
				{#if loading}
					<svg
						class="w-5 h-5 animate-spin"
						xmlns="http://www.w3.org/2000/svg"
						fill="none"
						viewBox="0 0 24 24"
					>
						<circle
							class="opacity-25"
							cx="12"
							cy="12"
							r="10"
							stroke="currentColor"
							stroke-width="4"
						/>
						<path
							class="opacity-75"
							fill="currentColor"
							d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"
						/>
					</svg>
				{/if}
				<span> SUBMIT </span></button
			>

			<a href={googleSheetUrl}>
				<button
					type="button"
					class="w-full md:w-[fit-content] flex items-center justify-center space-x-3  text-base font-semibold leading-none text-slate-600 py-4 px-10 bg-slate-200 rounded hover:bg-slate-300 focus:ring-2 focus:ring-offset-2 focus:ring-slate-700 focus:outline-none"
				>
					<span> VIEW SUBMISSIONS </span></button
				>
			</a>
		</div>

		{#if responseMessage}
			<p class="text-center mt-6 font-light leading-3 text-blue-500">
				{responseMessage}
			</p>
		{/if}
	</form>
</div>
