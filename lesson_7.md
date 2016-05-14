# Lesson 7

#### Goal

In this lesson, we'll be setting up a magic system! We'll create a listener that waits for us to type a spell into minecraft chat, and once a spell is typed, the script executes the python code corresponding to that spell!

#### New Concepts

In this lesson, we'll look at another for loop!

```python
for chatpost in mc.events.pollChatPosts():
    print chatpost
```

This code will execute the code inside the while loop once for every chat message found in the minecraft chat post since the last time we looked. By sticking this in an infinite while loop, we can actually watch all messages posted in chat, forever!

```python
if chatpost.message.lower() == "explode":
    print "explode was the message!"
```
You can use an if statement like this to test if the word explode IS the entire message.

```python
if "explode" in chatpost.message.lower():
    print "frank is inside the message!"
```
You can use an if statement like this to test if the word "explode" is anywhere in the message.

```python
who = chatpost.message.lower().split(' ')[1]
```
If you have a message where you are typing in a command AND a name (e.g. "explode joe"), this is how you extract the name joe and stick it in a variable. The code above will always extract the second word typed in a string (that what the 1 index is specifying).

#### Code
Open up script.py in a code editor. Delete everything in it, we'll be starting from scratch!

```python
from mcpi import minecraft
import time

server_address = "199.96.85.3"
my_player_name = "seanybob"

mc = minecraft.Minecraft.create(address=server_address, name=my_player_name)
```
These first few lines are similar to the previous lesson. Be sure to replace "seanybob" with your name!

```python
my_id = mc.getPlayerEntityId(my_player_name)
```
We first need to get our player ID, so we can focus on just listening to messages posted by us in chat

```python
print "Script started! Type in 'hi' or 'testing' in minecraft chat to activate. Hit command (or control) + C in your terminal to stop."
```
Let's add a print message to tell us when the script started.

```python
#Watch for chat messages
while True:

    #For each chat message since the last time we checked...
    for chatpost in mc.events.pollChatPosts():

        #Was the chat message sent by me?
        if chatpost.entityId == my_id:

            #if so, let's do something!
            if chatpost.message.lower() == "hi":
                mc.postToChat("Hello right back at you!")

            if chatpost.message.lower() == "testing":
                mc.postToChat("123")

    time.sleep(.1)
```
This is the foundation of our script! In an infinite while loop, we listen for chatposts. Whenever a chatpost is detected, we check if it was sent by us. If so, we check the contents of the message. If it matches one of the messages we are looking for, we execute python code!

#### Terminal

Run the script like so:
```shell
python script.py
```

# CHALLENGE 1

Add a new spell called "shield" that builds a glass shield "building" all around you, making it so nothing can attack you but you can still see. Hint: Refer to lesson 4

# CHALLENGE 2

Add a new spell called "nuke" that spawns several TNT around you. Spawn Fire (item ID 51) on or below the TNT to activate it. Make sure you spawn the TNT far enough away from you it doesn't kill you, but close enough it can take out your enemies!

# CHALLENGE 3

Add a new spell called "bird" that teleports you 100 blocks above your current position, waits 3 seconds, then teleports you back to your original position - thus giving you a bird's eye view of your current location.

# CHALLENGE 4

Using the player .getRotation() and .getPitch() functions, craft a new spell called "jumper" that teleports you several blocks forward in the direction you are looking. Consider checking if the location you are teleporting to is in the air, and spawning a block first under that position so you don't fall to your death.