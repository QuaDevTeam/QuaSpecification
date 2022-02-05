# Specification

## Project
Project is a folder with metadata file `meta.yml`, folder `resources`, and folder `scripts`
```
project
├───resources  
├───scripts
└───meta.yml
```

### Project Metadata
`meta.yml` contains all necessary information of this project.
```yaml
name: Game Name
author: XXX Studio
date: XXXX-XX-XX
langs:
    - zh-cn
# or langs: null
```

### Resources
All resources referenced in scripts must be in `resources` directory.
e.g.
```
resources
├───bgm
├───cgs  
├───characters  
├───scenes  
└───voices
```

## Scripts
If field `langs` in project metadata is null, then all scripts are directly stored in the `scripts` directory.
```
scripts
├───chapter1  
│    └───section1
├───index.js
└───meta.yml
```

If field `langs` in project metadata is specified, all scripts with different language must be stored in different folders with language name.
```
scripts
└───zh-cn
     ├───chapter1  
     │    └───section1
     ├───index.js
     └───meta.yml
```

### Script Metadata
```yaml
lang: zh-cn
entry: chapter1/section1
```

### Script Locate
Another script file can be refered using absolute path from the script root.
The root directory is the folder with language name.

### Script File
The QuaScript File has an extension name of `.qs`
The Control Flow is written in JavaScript.
```
meta.yml  
script.qs  
script.js
```

`meta.yml` specify the entry point of the script and other info
```yaml
name: section1
entry: section1-entry.qs
character:
  nanami:
    show: 七海
  mayu:
    show: 茉优
  satoru:
    show: 晓
    color: #fff
```

### Syntax
The QuaScript Syntax is very similar to YAML
```yaml
0:00:
    audio:
        - mayu:
            file: voices/mayu-25
        - background:
            file: bgm/background-13
            action: play
            repeat: true
    characters:
        mayu:
            file: characters/mayu-12
            action: show
            position: center
    scene:
        lab:
            file: scenes/lab-day
            transition: fade-in
0:02:
    characters:
        mayu:
            file: characters/mayu-13
0:04:
    characters:
        mayu:
            file: characters/mayu-14
mayu: 这稳定性真是了不得。感觉根本就不像是抓着人的手臂，而是像抓在树干上一样
```

### Basic Syntax
The script is composed of many pairs of Actions and Statements. Each pair of them is divided by a blank line.
```yaml
Action: Action1
Statement: Statement1

Action: Action2
Statement: Statement2

...
```

### Statement

#### Dialogue
```yaml
Character Name: Sentence
```
The short name of characters can be defined in meta.yml. It will be auto replaced by full name.

#### Narration
```yaml
Sentence
```

#### Selection
```yaml
select:
    options:
        - option1
        - option2
    event: select1
```

#### Input
```yaml
input:
	text: text1
	event: input1
```

#### Pause
```
pause: null

pause: 10s
```

### Action

Every action is many pairs of key:value, as key is the object name and value is the object parameters.
The key can refer to the object defined before and allows the action to modify its state.

#### Timeline
At every statement, the execution of the script will pause. Timeline is required so actions can be triggered when play the voice.
```yaml
0:00:
	actions
0:02:
	actions
```
If timeline is not needed, the actions can be directly placed in the root.

```yaml
actions: 
	- xxx
```

#### Audio
```yaml
audio:
    mayu:
        file: voices/mayu-25
    background:
        file: bgm/background-13
        action: play
        repeat: true # true when play background music
```

#### Characters (Sprites)
```yaml
characters:
    mayu:
        file: characters/mayu-12
        action: show
        position: center
```

#### Scene (Background)
```yaml
scene:
    lab:
        file: scenes/lab-day
        transition: fade-in
```

#### Event
```yaml
event:
    customEvent:
        - param1
```
Event is sent to Control Scripts

#### Draw
```yaml
draw:
    customDraw:
        - param1
```
Draw Event is sent to UI

### Parameters
#### File
`file` is the absolute path to find the resources
#### Action
`action` = start | change | stop
default is change
when the object is not defined (start) before, then change is start
stop can stop the performance of this object and destroy it.
#### Transition
`transition` is the effect when the object file change.
#### Position (Image Only)
#### Animation (Image Only)
#### Repeat (Sound Only)

