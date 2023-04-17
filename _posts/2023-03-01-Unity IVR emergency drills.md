---
tags: [Unity,C#,Quest2]
---
# IVR drills in Unity 3d

## Introduction


### Step 0
Getting used to Unity editor and implementing new basic features inside the demo 3d game.

### Step 1
Create a new project in order to improve fire and flood particle systems. The more realistc they are, the more engaging the drills will be. 

## Step 2
Adjust MidCoast hospital project details.

![hospital esterno](/assets/img/mid-coast-hospital.png)
![reception](/assets/img/mid-coast-hospital-reception.png)
![porte di emergenza](/assets/img/mid-coast-hospital-porte-emergenza.png)

### Step 3
Import the particle systems created inside the [Mid Coast Hospital](https://www.midcoasthealth.com/) project, adjust it (change some graphics, organize folders) and optimize the coding section.

### Step 4
Implement NPC (non-playable-character) clever movement in the surrounding environment.
  
  1. avoid walls collision
  2. declare some not-walkable areas (stairs, rooftop border, clinical rooms, entrance walls)
  3. add a property to all doors (nav mesh obstacle) to stop collisons with them
  4. on emergency signal: change NPC's behaviour and escape the damage sources (fire, water)
  5. on emergency signal: follow the nearest emergency exits

![nav obstacle](/assets/img/mid-coast-hospital-nav-mesh-obstacle.png)
![nav area](/assets/img/mid-coast-hospital-navigation-area.png)

### Step 5
Add a startmenu to select the hazard as well as future options.
![startmenu](/assets/img/main-menu.png)


