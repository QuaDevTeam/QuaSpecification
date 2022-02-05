```yaml
0:00:
	audio:
		- nanami:
			file: nanami-67
		- background:
			file: background-13
			action: start
			transition: fade-in 
			offset: 0:00
			repeat: true
			mute-when-play: nanami
	characters:
		nanami:
			file: nanami-12
			action: start
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
		dorm:
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
	event:
		customEvent:
			- param1
	draw:
		customDraw:
			- param1
nanami: Onii-chan Baka!!!

select:
	options:
		- choice 1
		- choice 2
		- choice 3
	event: select12

input:
	text: 请输入你的名字
	event: input2
```