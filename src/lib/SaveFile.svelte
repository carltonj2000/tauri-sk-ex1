<script lang="ts">
	import { save } from '@tauri-apps/api/dialog';
	import { invoke } from '@tauri-apps/api/tauri';

	async function handleSave() {
		try {
			const data = new FormData(this);
			const content = data.get('text');
			const path = await save();
			if (!path) return;
			await invoke('save_file', { path, content });
		} catch (err) {
			console.error(err);
		}
	}
</script>

<form on:submit|preventDefault={handleSave}>
	<textarea rows={7} name="text" />
	<button>Save File</button>
</form>
