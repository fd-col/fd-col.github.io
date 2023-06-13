---
tags: [Unity,C#,Quest2,emergency,drills]
---
# IVR drills in Unity 3d

## Introduction
This project is part of my **internship in Switzerland** and it is about _Immersive Virtual Reality_ in a medical environment to create a realistic tool that simulates an emergency evacuation status.


## Chapter 1

### Step 0
Getting used to Unity editor and implementing new basic features inside the demo 3d game.
![Unity](/assets/img/unity.png)

### Step 1
Create a new project in order to improve fire and flood particle systems. The more realistc they are, the more engaging the drills will be. 
![URP first project](/assets/img/test_URP_fire_flood.png)

## Chapter 2

### Step 2
Adjust MidCoast hospital project details.

![hospital esterno](/assets/img/mid-coast-hospital.png)
![reception](/assets/img/mid-coast-hospital-reception.png)
![porte di emergenza](/assets/img/mid-coast-hospital-porte-emergenza.png)

### Step 3
Import the particle systems created inside the [Mid Coast Hospital](https://www.midcoasthealth.com/) project, adjust it (change some graphics, organize folders) and optimize the coding section.

### Step 4
Implement NPC (non-playable-character) clever movement in the surrounding environment.
  
  - avoid walls collision
  - declare some not-walkable areas (stairs, rooftop border, clinical rooms, entrance walls)
  - add a property to all doors (nav mesh obstacle) to stop collisons with them
  - on emergency signal: change NPC's behaviour and escape the damage sources (fire, water)
  - on emergency signal: follow the nearest emergency exits

![nav obstacle](/assets/img/mid-coast-hospital-nav-mesh-obstacle.png)
![nav area](/assets/img/mid-coast-hospital-navigation-area.png)

### Step 5
Add a startmenu to select the hazard as well as future options.
![startmenu](/assets/img/main-menu.png)

### Step 6
Short video where the player enter the hospital while NPCs are moving around the environment; then, the emergency simulation starts and the player starts looking for a safe area.

[![](https://markdown-videos.deta.dev/youtube/XfwZfsfZNIY)](https://youtu.be/XfwZfsfZNIY)


## Chapter 3

### Step 7 
Start working on the definitive hospital. First of all, I tidied up all the Asset folder and tried to understand well what I already had and what I would had to implement in the future.


### Step 8
Redo all the navMesh surfaces (Floor,Walls,Rooftop,etc.) to handle NPCs movements.

![navmesh_newHospital](/assets/img/navmesh_hospital.png)


### Step 9
Ajust and optimaze certain hazard features, like: 
  - fire and smoke spreading among time and space
  - damage inflicted on the player entering the source of damage
  - change smoke particle system color after collision
  - scratch the doors around the fires areas
  - add audio sources on fires

![fire_drill](/assets/img/Unity-IVR-emergency-drills/hospital-fire-drill.png)
![particle_trigger](/assets/img/Unity-IVR-emergency-drills/particle_system_trigger1.png)

### Step 10 
Redo and adapt the menu to the new features, like multi-player selection. I choose a circular menu with icons inside the buttons to make it easy to use. The game starts directly inside the hospital with the default options selected, and thanks to the main menu is possible to change them by pressing the pause icon on screen. The options included are:
  1. Resume the game
  2. Stop the game
  3. Reload the game
  4. Activate or Descativate NPC in the hospital
  5. Choose which character you want to be 
  6. Select the type of hazard you will encounter.

![circular_menu_NPC](/assets/img/Unity-IVR-emergency-drills/hospital-circular-menu.png)
![circular_menu_Player](/assets/img/Unity-IVR-emergency-drills/hospital-circular-menu1.png)
![circular_menu_Hazard](/assets/img/Unity-IVR-emergency-drills/hospital-circular-menu2.png)

### Step 11
Occlusion culling feature implementation inside the simulation. 

Occlusion culling is a process which prevents Unity from performing rendering calculations for GameObjects that are completely hidden from view (occluded) by other GameObjects.

Every frame, Cameras perform culling operations that examine the Renderers in the Scene
and exclude (cull) those that do not need to be drawn. By default, Cameras perform frustum culling, which excludes all Renderers that do not fall within the Camera’s view frustum. However, frustum culling does not check whether a Renderer is occluded by other GameObjects, and so Unity can still waste CPU and GPU time on rendering operations for Renderers that are not visible in the final frame. Occlusion culling stops Unity from performing these wasted operations.

![occlusion_culling](/assets/img/Unity-IVR-emergency-drills/hospital-occlusion_culling.png)

