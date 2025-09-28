<% "---" %>
<%*
dv = app.plugins.plugins.dataview.api
const modalForm = app.plugins.plugins.modalforms.api;
const result = await modalForm.openForm("art-form");
const linkInfo = {
	links: ["https://shikimori.one/", "https://www.tvtime.com/", "http://www.world-art.ru/", "https://onikes.ru/", "https://yo8z6gv.github.io/", "https://www.animefillerlist.com/", "https://mangalib.me/", "https://ranobelib.me/", "https://anilib.me/", "https://senkuro.com/", "https://reyohoho.github.io/reyohoho/", "https://freetp.org/", "https://store.steampowered.com/"],
	names: ["shikimori", "tvTime", "worldArt", "onikes", "kesidatokioVods", "animeFillerList", "mangalib", "ranobelib", "animelib", "senkuro", "reyohoho", "freetp", "steam"],
	buttons: ["Shikimori", "TV Time", "World Art", "ONIKES", "KESIDATOKIO VOD'S", "Anime Filler List", "MangaLib", "RanobeLib", "AnimeLib", "Senkuro", "ReYohoho", "FreeTP", "Steam"],
}

let icon
switch (result.getData("Type")) {
	case "anime":
	case "anime film":
	case "cartoon":
		icon = "📺"
		break
	case "manga":
	case "manhua":
	case "manhwa":
		icon = "📗"
		break
	case "book":
	case "ranobe":
		icon = "📘"
		break
	case "course":
		icon = "🎓"
		break
	case "film":
		icon = "🎞"
		break
	case "game":
		icon = "🎮"
		break
	case "series":
		icon = "🎬"
		break
}

let title = tp.file.title
let num = dv.pages('"Text/Art"').filter(p => !p.file.path.includes('franchises') && !p.file.path.includes('templates') && !p.file.path.includes('ratings')).length
await tp.file.rename(`${title} (${result.getData("Flag")}${icon} ${num})`);


tR += `created: ${tp.date.now("YYYY-MM-DD[T]HH:mm:ssZ")}\n`
tR += `Cover: "!${result.getData("Cover").link}"\n`
tR += result.asFrontmatterString({ pick: [
    "Status",
    "Type",
    "Episode",
    "aliases",
    "Views",
    "Year",
    "Rating",
    "Season"
]});
-%>
<% "---" %>

# <% title %>

<%*
tR += `!${result.getData("Cover").link}`
-%>

<%*
let parser = null
//result.getData("Links")
//if (links[0].length > "https://shikimori.one/".length)
//	parser = await tp.user.shikimoriParser(tp, links[0])
%>


<%* // buttons
if (parser != null) {
	tR += "![]("
	tR += parser.imageLink
	tR += ")\n\n"
}

function createBtn(index, action) {
	tR += "\`\`\`button" + "\n"
	tR += "name " + linkInfo.buttons[index] + "\n"
	tR += "type link" + "\n"
	tR += "action " + action + "\n"
	
	// colors
	switch (linkInfo.names[index]) {
		case "shikimori":
			tR += "customColor \#4682b4" + "\n"
			break;
		case "tvTime":
			tR += "customColor \#997f00" + "\n"
			break;
		case "worldArt":
			tR += "customColor \#7a0000" + "\n"
			break;
		case "onikes":
			tR += "color purple" + "\n"
			break;
		case "kesidatokioVods":
			tR += "color purple" + "\n"
			tR += "customTextColor black" + "\n"
			break;
		case "animeFillerList":
			tR += "customColor \#da5100" + "\n"
			break;
		case "mangalib":
			tR += "customColor \#252527" + "\n"
            tR += "customTextColor \#b6720f" + "\n"
			break;
		case "ranobelib":
			tR += "customColor \#252527" + "\n"
            tR += "customTextColor \#2196f3" + "\n"
			break;
		case "animelib":
			tR += "customColor \#252527" + "\n"
            tR += "customTextColor \#7E57C2" + "\n"
			break;
		case "senkuro":
			tR += "customColor \#191A21" + "\n"
			break;
		case "reyohoho":
			tR += "customColor \#1c1c1c" + "\n"
			break;
		case "freetp":
			tR += "color green" + "\n"
			tR += "customTextColor black" + "\n"
			break;
		case "steam":
			tR += "customColor #133C6F" + "\n"
			tR += "textColor white" + "\n"
			break;
	}
	tR += "hidden true" + "\n"  
	tR += "\`\`\`" + "\n"
	tR += "^button-" + linkInfo.names[index] + "\n\n"
}

const links = result.getData("Links")
console.log(links.length)
for (let i = 0; i < links.length; i++) {
	let index = linkInfo.links.findIndex(link => links[0].includes(link))
	if (index == -1) {
		tR += "Not found link " + links[i] + "\n\n"
		continue
	}
	createBtn(index, links[i])
}
%>

<%* // inline buttons
for (let i = 0; i < links.length; i++) {
	let index = linkInfo.links.findIndex(link => links[0].includes(link))
	if (index == -1) {
		tR += "Not found link " + links[i] + "\n\n"
		continue
	}
	if (i % 2 == 0)
		tR += `\n\`button-${linkInfo.names[index]}`
	else
		tR += ` \`button-${linkInfo.names[index]}`
}
%>

## Причина добавления




## Описание

<%*
if (parser != null) {
	tR += parser.desc
}
%>
