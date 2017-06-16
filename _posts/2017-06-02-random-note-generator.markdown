---
layout: post
title:  "Random Note Generator"
date:   2017-06-02 8:15:13 -0600
categories: jekyll update
---
<div id="noteGenerator">
	<div id="note"></div>
	<button id="generate" class="bigButton">Random Note</button>
	<button id="accidentalToggle" class="bigButton">Allow Sharps/Flats</button>
	<div class="interval">
		<h3>Auto-Update</h3>
		New note every <input id="changeInterval" type="text" placeholder="30" /> seconds. 
		<button id="startInterval">Start</button>
		<button id="stopInterval">Stop</button>
	</div>
</div>

<link href="https://fonts.googleapis.com/css?family=Raleway:200,400,600,900" rel="stylesheet">

<style>
#noteGenerator {
    font-family: 'Raleway', sans-serif;
    text-align: center;
    border: 1px solid gray;
    display: block;
    padding: 10px 50px;
    width: 350px;
    margin: 20px auto;
}

h1 {
	margin-top: 15px;
	font-size: 32px;
	font-weight: 200;
}

button, input {
	font-family: 'Raleway', sans-serif;
	font-weight: 400;
}

button {
	border: 1px solid #ccc;
	background: #eee;
	outline: none;
}

button:active,
button.active {
	border: 1px solid #aaa;
	background: #ddd;
	outline: none;
	box-shadow: inset 0 1px 3px #aaa;
}

.bigButton {
	padding: 8px 15px;
	font-size: 16px;
}

#note {
	height: 300px;
	font-size: 140px;
	line-height: 260px;
	font-weight: 900;
}

h3 {
	font-weight: 600;
	margin-bottom: 10px;
}

.interval {
	margin: 40px 0;
}

#changeInterval {
	width: 60px;
	font-weight: 600;
	padding: 3px;
}
</style>

<script>
class RandomNoteGenerator {
	constructor() {
		// Resources
		this.noteSet = ['A', 'B', 'C', 'D', 'E', 'F', 'G']
		this.accidentalSet = ['#', '', 'b']
		
		// Defaults
		this.allowAccidentals = false
		this.intervalRunning = false
		this.duration = 3
		this.interval = null
		
		// Elements
		this.noteDiv = document.getElementById('note')
		this.generateButton = document.getElementById('generate')
		this.accidentalToggle = document.getElementById('accidentalToggle')
		this.startIntervalButton = document.getElementById('startInterval')
		this.stopIntervalButton = document.getElementById('stopInterval')
		this.intervalInput = document.getElementById('changeInterval')
		
		// Event Listeners
		this.generateButton
			.addEventListener('click', this.generate.bind(this))
		this.accidentalToggle
			.addEventListener('click', this.toggleAccidentals.bind(this))
		this.startIntervalButton
			.addEventListener('click', this.startInterval.bind(this))
		this.stopIntervalButton
			.addEventListener('click', this.stopInterval.bind(this))
		
		this.generate()
		this.intervalToggleMarkup()
		
	}

	generate() {
		let note = this.getNote(this.noteDiv.innerHTML)
		this.noteDiv.innerHTML = note
	}
	
	getNote(previousNote) {
		let accidental = null;
		let note = this.randomNote()
		if (this.allowAccidentals) {
			note = note + this.randomAccidental()
		}
		// Use recursion to make sure we always have a new note
		if (previousNote == note) {
			return this.getNote(note)
		} else {
			return note
		}
	}
	
	randomNote() {
		let index = Math.floor(Math.random() * 7)
		return this.noteSet[index]
	}
	
	randomAccidental() {
		let index = Math.floor(Math.random() * 3)
		return this.accidentalSet[index]
	}
	
	toggleAccidentals() {
		this.allowAccidentals = !this.allowAccidentals
		if (this.allowAccidentals) {
			this.accidentalToggle.classList.add('active')
		} else {
			this.accidentalToggle.classList.remove('active')
		}
	}
	
	startInterval() {
		// Update interval
		this.duration = Number(this.intervalInput.value) ? Number(this.intervalInput.value) : 30
		// Clear previous intervals, so only one will run at a time
		clearTimeout(this.interval)
		// start a new interval
		this.intervalRunning = true
		this.recursiveGenerate()
		
		this.intervalToggleMarkup()
	}
	
	recursiveGenerate() {
		if (this.intervalRunning) {
			this.generate()
			
			this.interval = setTimeout(
				()=>{
					this.recursiveGenerate()
				},
				(this.duration * 1000)
			)
		}
	}
	
	stopInterval() {
		this.intervalRunning = false
		this.intervalToggleMarkup()
	}
	
	intervalToggleMarkup() {
		if (this.intervalRunning) {
			this.startIntervalButton.classList.add('active')
			this.stopIntervalButton.classList.remove('active')
		} else {
			this.startIntervalButton.classList.remove('active')
			this.stopIntervalButton.classList.add('active')
		}
	}
}
randomNoteGenerator = new RandomNoteGenerator()
</script>