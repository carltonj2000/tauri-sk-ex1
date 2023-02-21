<script lang="ts">
	import { open } from '@tauri-apps/api/dialog';
	import { readTextFile } from '@tauri-apps/api/fs';
	import Greet from '../lib/Greet.svelte';
	import SaveFile from '../lib/SaveFile.svelte';
	import WriteFile from '../lib/WriteFile.svelte';

	const readFileContents = async () => {
		try {
			const selectedPath = await open({
				multiple: false,
				title: 'Open a file'
			});
			if (!selectedPath) return;
			const fileData = await readTextFile(selectedPath);
			console.log(fileData);
		} catch (err) {
			console.error(err);
		}
	};
</script>

<h1>Welcome to Tauri And SvelteKit</h1>
<Greet />

<button on:click={readFileContents}>Open File Explorer</button>

<SaveFile />
<WriteFile />
