<%*
const files = tp.app.vault.getMarkdownFiles()
for (let i = 0; i < files.length; i++) {
	let file = files[i]
	await tp.app.fileManager.processFrontMatter(file, (fm) => {
		if (fm["modified"] == null) return
		delete fm["modified"]
	})
}
%>