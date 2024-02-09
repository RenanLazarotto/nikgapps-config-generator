<script lang="ts">
	const androidVersions = [
		{ label: 'Android 14 (U)', value: '14' },
		{ label: 'Android 13 (T)', value: '13' },
		{ label: 'Android 12L (SL)', value: '12L' },
		{ label: 'Android 12 (S)', value: '12' },
		{ label: 'Android 11 (R)', value: '11' },
		{ label: 'Android 10 (Q)', value: '10' }
	];
	let selectedVersion: string;
</script>

<form class="grid grid-cols-12 gap-4">
	<div class="col-span-12 sm:col-span-6 lg:col-span-5">
		<h1 class="text-4xl font-black py-4">NikGapps Config Generator</h1>
		<p class="mb-4">
			This is a simple tool that helps you generate a custom <code>nikgapps.config</code> file to generate
			a custom NikGapps build.
		</p>

		<label class="form-control mb-2">
			<div class="label">
				<span class="label-text font-bold">Select the target Android version</span>
			</div>
			<select
				class="select select-sm select-bordered"
				name="androidVersion"
				bind:value={selectedVersion}
			>
				<option disabled selected>Pick one</option>
				{#each androidVersions as version}
					<option value={version.value}>{version.label}</option>
				{/each}
			</select>
		</label>

		<details open>
			<summary>Advanced setttings</summary>

			<div class="grid grid-cols-1 md:grid-cols-2 gap-2">
				<div class="md:mb-2">
					<label class="form-control mb-2">
						<div class="label">
							<span class="label-text font-bold"> Where the logs should be stored? </span>
						</div>
						<input
							type="text"
							name="log-directory"
							class="input input-sm input-bordered"
							value="default"
						/>
					</label>

					<label class="form-control mb-2">
						<div class="label">
							<span class="label-text font-bold">Where the Gapps should be installed?</span>
						</div>
						<input
							type="text"
							name="install-directory"
							class="input input-sm input-bordered"
							value="default"
							list="install-locations"
						/>
						<datalist id="install-locations">
							<option value="/system">/system</option>
							<option value="/product">/product</option>
							<option value="/system_ext">/system_ext</option>
						</datalist>
					</label>

					<label class="form-control mb-2">
						<div class="label">
							<span class="label-text font-bold">Install mode</span>
						</div>
						<select class="select select-sm select-bordered mb-1" name="mode">
							<option value="install" selected>Install Gapps</option>
							<option value="uninstall">Uninstall Gapps</option>
						</select>
						<div class="label-text-alt">
							Select 'Uninstall' if you want to uninstall any Google app. Please also set the value
							of the app to -1 on the package selection.
						</div>
					</label>

					<label class="form-control mb-2">
						<div class="label">
							<span class="label-text font-bold">Wipe Dalvik cache?</span>
						</div>
						<select class="select select-sm select-bordered mb-1" name="mode">
							<option value="1" selected>Wipe</option>
							<option value="0">Don't wipe</option>
						</select>
						<div class="label-text-alt">
							Select if you want the installer to wipe dalvik/cache after installing the Gapps.
						</div>
					</label>

					<label class="form-control">
						<div class="label">
							<span class="label-text font-bold">Wipe runtime permissions?</span>
						</div>
						<select class="select select-sm select-bordered mb-1" name="mode">
							<option value="1" selected>Wipe</option>
							<option value="0">Don't wipe</option>
						</select>
						<div class="label-text-alt">
							Select if you want the installer to want to wipe runtime permissions.
						</div>
					</label>
				</div>

				<div>
					<label class="form-control mb-2">
						<div class="label">
							<span class="label-text font-bold">Create execute.d config?</span>
						</div>
						<select class="select select-sm select-bordered mb-1" name="mode">
							<option value="1" selected>Yes</option>
							<option value="0">No</option>
						</select>
						<div class="label-text-alt">
							Select if you want to create addon.d config, used to persist Gapps package on ROM
							updates. Select 'no' to skip the automatic backup/restore while flashing the ROM.
						</div>
					</label>

					<label class="form-control mb-2">
						<div class="label">
							<span class="label-text font-bold">Use ZIP config?</span>
						</div>
						<select class="select select-sm select-bordered mb-1" name="mode">
							<option value="1" selected>Yes</option>
							<option value="0">No</option>
						</select>
						<div class="label-text-alt">
							Select if you want to force the installer to use the config from Gapps zip file.
						</div>
					</label>

					<label class="form-control">
						<div class="label">
							<span class="label-text font-bold">Enable GMS optimization?</span>
						</div>
						<select class="select select-sm select-bordered mb-1" name="mode">
							<option value="1" selected>Yes</option>
							<option value="0">No</option>
						</select>
						<div class="label-text-alt">
							Select if you want to enable GMS (Google Mobile Services) optimization. Attention:
							careful while doing it, you may experience issues like delayed notification with some
							ROMs.
						</div>
					</label>
				</div>
			</div>
		</details>
	</div>

	<div class="col-span-12 sm:col-span-6 lg:col-span-7">
		<h2 class="text-4xl font-black py-4">Package selection</h2>
	</div>
</form>
