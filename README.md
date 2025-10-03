# Building-vehicle-hobby-project

Hello this is a hobby proejct where my goal was to build your own car and save it for gameplay. 

Before I go into all steps I jsut want to summerize the functions here
I can place and rotate objects 
Saving them so they know their neghboors 
Seting their constraints
Save/Load with constraints

# Calculation of face and target cube

I have a blueprint called main build. This blueprint is parent of all different building type. In this case cube, wheel and weapon. This blueprint have collider in each side. 
<img width="769" height="526" alt="image" src="https://github.com/user-attachments/assets/49f3cff0-78e8-45d6-bf47-ae2a9268d69b" />

After some checks with bool I run this function. I get the forward vector of the collider and make a rotation from that forward vector. With the angle input I can manipulate the offset 
value. This variable changes from input and this leads this object to rotate free.  
<img width="745" height="425" alt="image" src="https://github.com/user-attachments/assets/7722bf45-df39-4964-91ff-34de679637d2" />

# Occupy sides
Then to not add multiple cubes in one side I made a occupation system. It holds a map of all colliders around the cube and I hold them all in a map. After I build on one side
I mark it as false. Here in preview I find the same collider with tag and checks if the bool is true or not. If its true then is is occupied so i change the color of it. 
<img width="776" height="355" alt="image" src="https://github.com/user-attachments/assets/8fa190a3-8ce1-4be9-92b1-0a3b58c7f35b" />

![occupied-ezgif com-optimize](https://github.com/user-attachments/assets/199753b2-c277-4f08-9bba-97f2396a5730)

# Constraints
I wanted them to be connected together through constraints. For that I needed a system to let them know the object they will have their parents to. After some debuging I came up with the idea. Every spawned object should have a index number. Every time I spawn a cube on another cube "the cube I am hovering my mouse over" becomes the one that is attached to the ne cube. That makes that cube parent automaticly. So I set the parent index from the parent cubes actor index number. 

<img width="635" height="301" alt="image" src="https://github.com/user-attachments/assets/6a31eb82-2a51-4bf0-81e4-cb7fa638a95f" />




