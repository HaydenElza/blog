---
date: 2015-06-27
layout: post
slug: 
title: "Minecraft: Teleportation Book"
categories:
- Minecraft
tag:
- teleport
- warp
- minecraft
- raw json
---

[![](https://i.imgur.com/iftTEYeh.png)](https://i.imgur.com/iftTEYe.png)

### Setup Objective

Start by adding a new objective by copying and pasting the following code into chat:

~~~
/scoreboard objectives add teleport trigger
~~~

### Create Book

Next we create the book that players can read and click to run commands. You will need to copy and paste the code into a command block as it is too long to run in chat. I like to keep a command block around with a button on it to give me a book when ever I need one rather than copying each time a new player comes on the server.

~~~json
/give @p minecraft:written_book 1 0 {
title:"Warp",
author:"",
pages:[
	"{text:\"Warps: \",color:dark_gray,extra:[
		{
			text:\"\n Spawn \",
			clickEvent:{
				action:run_command,
				value:\"/trigger teleport set 1\"
			}
		},
		{
			text:\"\n Storage \",
			clickEvent:{
				action:run_command,
				value:\"/trigger teleport set 2\"
			}
		},
		{
			text:\"\n Slime Farm  \",
			clickEvent:{
				action:run_command,
				value:\"/trigger teleport set 3\"
			}
		}
	]}"
]}
~~~

### Redstone Clock

Each command below needs to placed on the same redstone clock to constantly run.

~~~
/scoreboard players enable @a teleport

/scoreboard players set @a[score_teleport_min=1] teleport 0

/tp @p[score_teleport_min=1,score_teleport=1] 391 56 -555
~~~

The first command enables players to use the trigger. This needs to constantly run because a trigger needs to be re-enabled for a player after each use. The seccond comand tests for a "teleport" score greater than 0 and will reset a players "teleport" score back to zero. The last command is what ever command you want to run when the trigger is set to 1. Below are examples of commands for a "teleport" trigger set to 2 and 3.

~~~
/tp @p[score_teleport_min=2,score_teleport=2] 321 12 -325

/tp @p[score_teleport_min=3,score_teleport=3] -564 63 112
~~~

My layout for the clock is pictured below. Notice that all of the command blocks are on the same side of the clock. This is required for reliable use.

[![](https://imgur.com/BnqAi2Wh.png)](https://imgur.com/BnqAi2W.png)

### Stop commands from displaying in console

Enabling the trigger for everyone on a clock will spam chat for ops. We can avoid this by using the following command to suppress command block messages in chat:

~~~
/gamerule commandBlockOutput false
~~~

---
<br>
I hope this helps. If you have any questions you can find me on twitter. Happy gaming!
