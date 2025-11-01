Project: zuul-bad
Authors: Michael Kölling and David J. Barnes

This project is part of the material for the book

   Objects First with Java - A Practical Introduction using BlueJ
   Seventh edition
   David J. Barnes and Michael Kölling

This project is a simple framework for an adventure game. In this version,
it has a few rooms and the ability for a player to walk between these rooms.
That's all.

To start this application, create an instance of class "Game" and call its
"play" method.

This version of the game contains some very bad class design. It should NOT
be used as a basis for extending the project without fixing these design
problems. It serves as an example to discuss good and bad design (chapter 8
of the book).

Chapter 8 of the book contains a detailed description of the problems in this
project, and how to fix them.

The project 'zuul-better' contains a version of this project with better
designed class structure. It includes the fixes discussed in the book.
LAB 8
Part I: zuul-bad
1. 
- This appilcation allows you to go from room to room.
- The commands accepted are "go", "quit" and "help".
- The "go" command allows the player to go from room room to another but it has to say "go" + direction fot the game to understand. The command "quit" allows the player to leave the game and "help" give the player the command word he can use to play the game. 
There are 4 actual rooms and if we count the outside as a room then 5. 
pub <-> outside <-> theatre
           ^
           |
           v
          lab <-> office
2. 
Game: It creates all rooms and the parser. It starts the game. It executes commands returned by the parser. 
Parser: It checks the user input with the command words he has and if it does not match then it returns an uknown command.
Command: If the first word or the second word is wrong then it returns null because he didn't recognize it
CommandWords: It holds all the valid command words and it recognizes it when it is typed.
Room: The class defines all the exists. It returns null if there are no exists in that direction. It also gives the description of the room you are in.

3. The player has to go from room to find a treasure chest.

4. 
            Chamber
               |
            Library
               |
Main Hall - Kitchen - Treasure Room
               |
           Basement
private void createRooms(){
Room mainHall, kitchen, library, chamber, treasureRoom, basement;
mainHall = new Room("in the main hall");
kitchen = new Room("in the kitchen ");
library = new Room("in the library");
chamber = new Room("in the chamber");
treasureRoom = new Room("in the treasureRoom");
basement = new Room("in the basement");

mainHall.setExit("east", kitchen);
kitchen.setExit("west", mainHall);
kitchen.setExit("east", treasureRoom);
kitchen.setExit("north", library);
kitchen.setExit("south", basement);
library.setExit("up", chamber);
chamber.setExit("down", library);
treasureRoom.setExit("west", kitchen);
basement.setExit("up", kitchen);

currentRoom = mainHall;
}

9.Returns a Set view of the keys contained in this map. 

12. 
pub <-> outside <-> theatre
           ^
           |
           v
          lab <-> office
           |        |
           v        v
         library   basement

13. The state of the currentRoom changes. It starts with currentRoom = outside but if we type go east,the currentRoom = theater.

17. No, you dont because the Game class doesnt contain the list of commands. Since the commandWords knows all the valid commands, the Game class can access it through the parser with the showCommands method. 

18. I think it makes sense to make the methods in CommandWords static because we do not have to create an object for that class to use it but a con for it is that it will harder to change if we put multiple sets of commands. Static is less flexible while instance is more flexible. Not sure
