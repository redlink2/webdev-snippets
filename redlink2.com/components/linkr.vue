<template>
	<div class="flexy">
		<div class="links" id="left">
			<div class="bound">
				<img
					:style="{ filter: hueRotate + hue1 + suffix }"
					:src="require(`~/assets/circle.svg`)"
					v-on:click="linkset1"
					id="fit"
				/>
			</div>
		</div>
		<div class="links" id="center">
			<div class="bound">
				<img
					:style="{
						color: rgb + color1 + comma + color2 + comma + color3 + suffix
					}"
					:src="require(`~/assets/tri.svg`)"
					v-on:click="linkset2"
					id="fit"
				/>
			</div>
		</div>
		<div class="links" id="right">
			<div class="bound">
				<img
					:style="{ filter: hueRotate + hue3 + suffix }"
					:src="require(`~/assets/square.svg`)"
					v-on:click="linkset3"
					id="fit"
				/>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	mounted() {
		var link1 = document.querySelector('#link1')
		var link2 = document.querySelector('#link2')
		var link3 = document.querySelector('#link3')
		// rand gen hue1/2/3
		this.hue1 = Math.floor(Math.random() * 333)
		this.hue2 = Math.floor(Math.random() * 333)
		this.hue3 = Math.floor(Math.random() * 333)
	},
	methods: {
		linkset1() {
			link1.innerHTML = `<a href="` + this.github[0] + `">` + this.github[1] + `</a>`
			link2.innerHTML = `<a href="` + this.jelly[0] + `">` + this.astral[1] + `</a>`
			link3.innerHTML = `<a href="` + this.sidebar[0] + `">` + this.sidebar[1] + `</a>`
		},
		linkset2() {
			link1.innerHTML = `<a href="` + this.jelly[0] + `">` + this.jelly[1] + `</a>`
			link2.innerHTML = `<a href="` + this.pihole[0] + `">` + this.pihole[1] + `</a>`
			link3.innerHTML = `<a href="` + this.router[0] + `">` + this.router[1] + `</a>`
		},
		linkset3() {
			link1.innerHTML = `<a href="` + this.proton[0] + `">` + this.proton[1] + `</a>`
			link2.innerHTML = `<a href="` + this.codecad[0] + `">` + this.codecad[1] + `</a>`
			link3.innerHTML = `<a href="` + this.mega[0] + `">` + this.mega[1] + `</a>`
		},
	},
	data() {
		return {
			//hue-rotate randomizer
			rgb: "rgb(",
			color1: 0,
			color2: 0,
			color3: 0,
			suffix: ")",
			comma: ",",
			//tab1
			github: ["https://github.com", "Github"],
			astral: ["https://app.astralapp.com", "Astral"],
			sidebar: ["https://sidebar.io", "Sidebar"],
			//tab2
			jelly: ["http://10.0.0.8:8096", "Jellyfin"],
			pihole: ["http://10.0.0.22/admin", "PiHole"],
			router: ["http://10.0.0.1", "Router"],
			//tab3
			proton: ["https://mail.protonmail.com", "ProtonMail"],
			codecad: ["https://codecademy.com/learn", "Codecademy"],
			mega: ["https://mega.nz", "Mega"],
		}
	},
}
</script>

<style scoped>
.flexy {
	height: 100%;
	width: 100%;
	display: flex;
	flex-direction: row;
	align-items: center;
}
.bound {
	height: 100%;
	width: 100%;
	display: flex;
	flex-direction: row;
	align-items: center;
	justify-content: center;
}
#fit {
	display: flex;
	width: 50%;
	height: 50%;
	filter: hue-rotate(0deg);
}
#fit:hover {
	cursor: pointer;
}
@keyframes slide-in {
	0% {
		transform: rotate(0turn);
	}
	50% {
		filter: hue-rotate(180deg);
	}
	100% {
		transform: rotate(1turn);
	}
}
#fit:active {
	animation: slide-in 1000ms;
}
.links {
	height: 100%;
	width: 100%;
	border-style: ridge;
	border-top: 2px;
	border-bottom: 2px;
	display: flex;
	align-items: center;
	flex-direction: column;
	justify-content: center;
}
#left {
	border-color: cyan;
}
#center {
	border-color: magenta;
}
#right {
	border-color: yellow;
}
.li {
	padding: 20px;
}
</style>