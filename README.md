# GildedUpgrade 
[Discord for quick help](https://discord.gg/VatBrmDwmf)
### Quick start:

### 1. Make a generator
There are two required entries in a generator. it's value and material.
The name of generator file when the extension is removed is the id of the generator.
There is a sample generator generated when the plugin is first loaded. You can refer to it.
#### 2. Make a tree
Use the line ID to represent the whole line.
The line ID is the ID of the generator with "li-" in front.
Lines at the end of the upgrade string must be marked "end".
The following lines are children of the previous line. A line can have multiple sublines.
Each tree must have only 1 line on the first level as the root for the plugin to work properly.
### 3. Load
Everything is automatically loaded when the plugin is active or when you use the load command.

### Mechanic:
### 1. What is value?
Each item or socket has a value. This value is used to calculate the probability of successful
upgrade of the item. The rate of success is calculated as follows:
- x is the average value of the current level and the next levels
- Y is the value of socket
- C is the success rate. Default is ZERO.
- C = C + ( 100 - C ) * ( Y / ( Y + X ) )
- The rate is calculated on each socket one by one until the end.
- For example, let's take an item A with a value of 100. Get three more sockets with values
- 50, 100 and 75 respectively.
- Default rate is 0.
- Start with the one with the value is 50. 0+(100-0)*(50/(50+100)) -> Rate is now 33,(3)%
- Continue with the one whose value is 100. 33,(3)+(100-33,(3))*(100/(100+100)) -> Rate is now 66,(6)%
- Continue with the one whose value is 75. You can calculate it yourself ;) (Rate is now 80,95%)
#### 2. What is ticket? <removed>
A final level item can be upgraded to one or more different items. The ticket will ensure that
the item is upgraded to the first item in the line with the same id as the ticket's id.
Very simple. Right?
#### 3. What if I want to edit an item that has already been released?
When you edit the generator then reload, when the player clicks any item on the inventory,
the items created by that generator will change accordingly. Similarly, when you don't want
the player to use that series of items anymore, you can tweak the generator to turn that whole
series of items into something useless. ;)
### Syntax:
###### Tree
The trees are configured in the config.yml file.
It is very simple. Let me take an example:
```tr-Sword:
li-Wooden_Sword:
  li-Iron_Sword:
    li-Wakizashi: end
    li-Oodashi: end
    li-Nagamaki: end
    li-Naginata: end
  li-Steel_Sword: end
```
As you can see, a tree starts with the ID of that tree. For some reason the tree ID must start with "tr-". Then we add the lines in turn. These lines will be automatically generated based on the generator corresponding to the ID of that line. The lines at the end, ie the lines that cannot be upgraded any more, must be marked "end" (you can write anything, not necessarily is "end". But don't leave it blank).
2. Generator:
Everything is already in the file "Example.yml" but now I will explain it better. As mentioned in the quick start, the two essential components of a generator are material and value. Generator will not be loaded if these two items are missing.

###### Let's start with "Level".
* Level is level of item.
* Level is represented by "{level}".
* Level is a natural number starting from 1.
That's all. Yes, it's very simple.
###### Next is the Script.
The script is placed between two @ character.
Script with syntax based on JavaScript language
Scripts must return float or int values depending on where you use them. In particular
there are some places where the Script will not work properly without returning an int
such as value, enchant level or Custom Model Data. At these places the value will be
rounded to int.
###### Storage ?
This is just a file for the plugin to store items and lines. You'd better not touch
them if you don't want to get in trouble.
