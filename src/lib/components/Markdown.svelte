<script>
	import { marked } from 'marked';
	import hljs from 'highlight.js';
	import 'highlight.js/styles/github.css';

	marked.setOptions({
		highlight: function (code, lang) {
			const language = hljs.getLanguage(lang) ? lang : 'plaintext';
			console.log(language);
			console.log(hljs.highlight(code, { language }).value);
			return hljs.highlight(code, { language }).value;
		}
	});

	let source = ``;
	$: markdown = marked.parse(source);
</script>

<div class="markdown-editor">
	<textarea bind:value={source} class="source" />

	<div class="output">{@html markdown}</div>
</div>

<style type="scss">
	.markdown-editor {
		position: relative;
		width: 100%;
		min-height: 90vh;
		display: grid;
		grid-template-columns: 1fr 1fr;

		textarea {
			border: none;
			box-shadow: none;
			resize: none;
			outline: none;
			background-color: var(--background-primary);
		}

		textarea,
		.output {
			padding: 30px;
		}

		.output {
			border-left: 2px solid var(--clr-secondary);
		}
	}
</style>
