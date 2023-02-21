<script lang="ts">
	import { BaseDirectory, writeTextFile } from '@tauri-apps/api/fs';

	async function handleSave() {
		try {
			const data = new FormData(this);
			const { content } = Object.fromEntries(data);
			if (!content) return;
			await writeTextFile('test.txt', content.toString(), {
				dir: BaseDirectory.Download
			});
		} catch (err) {
			console.error(err);
		}
	}
</script>

<form on:submit|preventDefault={handleSave}>
	<textarea rows={7} name="content" />
	<button>Save File</button>
</form>
