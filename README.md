# Simple building system

![3-ezgif com-optimize](https://github.com/user-attachments/assets/f40891bc-f8a9-4395-a1cb-578dd98c22c8)Building Vehicle Hobby Project

### Hello!
This is a hobby project where my goal was to create a modular vehicle-building system that lets players construct and save their own cars.

The system allows:

- Placing and rotating objects using raycasts

- Tracking occupied sides to prevent overlapping

- Connecting parts using physics constraints

- Saving and loading objects (including constraints)

To make the building system, I used raycasts extensively. The system technically works like this:
Each cube has colliders on every side. 

<img width="906" height="530" alt="image" src="https://github.com/user-attachments/assets/212e98b0-5cb0-46d6-bf6d-5eda17392db5" />


I send a raycast to the cube, and the collider that gets hit becomes the area where a new part can be spawned. I then calculate the center of that collider and place the new object there if the spot is free.

Step by step:
First, I have a Blueprint called Main Build, which is the parent class for all different building types (cube, wheel, and weapon).

<img width="769" height="526" alt="image" src="https://github.com/user-attachments/assets/49f3cff0-78e8-45d6-bf47-ae2a9268d69b" />

After some boolean checks, I run this function. It gets the forward vector of the collider and creates a rotation based on that vector. With an input angle, I can manipulate the offset value. This variable changes dynamically from player input, allowing the object to rotate freely.

<img width="745" height="425" alt="image" src="https://github.com/user-attachments/assets/7722bf45-df39-4964-91ff-34de679637d2" />
Occupy Sides

To prevent adding multiple cubes to the same side, I created an occupation system. It stores all colliders around the cube inside a map. After building on one side, I mark that entry as occupied.

In preview mode, I find the collider by its tag and check if the corresponding boolean in the map is true or false.

If true → the side is occupied, and I change the preview color to red.

If false → the side is free, and placement is allowed.

<img width="776" height="355" alt="image" src="https://github.com/user-attachments/assets/8fa190a3-8ce1-4be9-92b1-0a3b58c7f35b" />

Constraints

I wanted the cubes to connect using constraints. For that, I needed a system to identify which cube should become the parent of a new piece.

After some debugging, I came up with a simple idea:
Each spawned object receives a unique index number. When a new cube is placed on another, the cube I’m hovering over becomes the parent automatically. The new cube stores its parent’s index so I can rebuild these relationships later.

<img width="635" height="301" alt="image" src="https://github.com/user-attachments/assets/6a31eb82-2a51-4bf0-81e4-cb7fa638a95f" />
Save and Load

This was the most challenging part. Initially, I tried saving the entire actor, but when loading, the actors didn’t appear in the scene and Unreal crashed instantly.

After a week of debugging, I changed my approach. Instead of saving the actor itself, I now save its class and transform (location, rotation, scale). When loading, I simply spawn new instances using that data.

<img width="719" height="443" alt="image" src="https://github.com/user-attachments/assets/c231446d-cb24-49a4-a129-49f4335287fd" />

Another problem was that Unreal didn’t allow me to save arrays directly. My solution was to create a temporary array to collect all the data, and then save that array to the file.

Here, I save all arrays into the save file:

<img width="920" height="260" alt="image" src="https://github.com/user-attachments/assets/299b6e3f-f3ce-4eae-8f97-3ed57ba7d3d8" />

This is the result
With the save button I save the cubes and load them in another scene
![3-ezgif com-optimize](https://github.com/user-attachments/assets/8aa13513-0626-4e76-9657-3aacec083da9)

THis of course work with wheels too
![4-ezgif com-optimize (1)](https://github.com/user-attachments/assets/890d6749-08f5-4efb-8c7c-3a05fb8c0f21)

This project was originally part of a game idea I worked on with a friend, but we later changed direction, so I decided to end development. Still, I learned a lot about Unreal Engine — especially raycasting, constraints, and data saving systems. There are many areas I’d like to explore further, particularly improving save/load workflows.

Thank you for reading.

