```yaml
0:00:
	audio:
		- nanami-67
		- background:
			file: background-13
			action: play
			transition: fade-in 
			offset: 0:00
	characters:
		nanami:
			file: nanami-12
			action: show
			position: center
			transition:
				- name: fade-in
			animation:
				- shake:
					action: start
					fadein: 1.0s
				- move:
					action: start
					duration: 1.0s
					distance: 50px
					direction: right
					curve: ease-out
	scene:
		file: dorm-2
		position: top
		size: cover 
		transition: fade-in
		animation:
			- move
0:02:
	characters:
		nanami:
			action: modify
			file: nanami-17
			animation:
				- shake:
					action: stop
	custom:
		customEffect:
			- effect-123
nanami: Onii-chan Baka!!!
			
```