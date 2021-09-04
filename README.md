# Unity Live Project - Code Summary
## <a name="intro"></a>Introduction
I took part in a 2-week sprint for the Live Project as part of the Tech Academy's Game Development Bootcamp. During this live project I made a version of the classic arcade game Space Invaders using Unity and C#. Creating a game from scratch was a great experience in learning both the Unity editor and C#. Through this experience I have become familiar in not only how to navigate the Unity Editor but also in utilizing Unity components and game objects. I also gained experience in manipulating Unity game objects with C#. More specifically, I created C# scripts for each feature of the game and within those scripts, I utilized built-in functions, conditional statements, and more. <br>
Furthermore, the live project was a great way to experience what it is like to work in a collaborative environment as it made use of Agile/Scrum methodology and DevOps.  Throughout this sprint, I took part in daily standup meetings, a sprint planning, and two sprint retrospectives. Communication was also a key part of this sprint in that, not only were there daily standups, but I also sent daily reports to the project manager to keep track of my progress. Additionally, I completed this project by resolving user stories that were assigned to me through Azure DevOps. <br>
I also gained experience in version control as I used GitHub desktop to create a branch for each story, merge the master to the branch daily, commit and push changes to the remote branch, and resolve any merge conflicts that occurred. When I resolved a story, I would create a pull request through Azure DevOps, link the pull request to the particular story, and move my story to the resolved column in the Board so that the instructors could review and either approve my pull request or move it back into the Active column with feedback for more changes. <br>
Overall, through this live project, I was able to experience what it was like to work in a collaborative Agile/Scrum environment. I also gained experience in utilizing the Unity editor and in Object Oriented Programming with C#. Additionally, I learned the importance of committing frequently and describing code in detail. Below is a summary of each story I resolved with code snippets and gifs to illustrate the features of the game and the code of the functionalities implemented. The folders and files in this repository hold more in-depth code snippets and gifs.
### Folder navigation:
* [Finalized game code snippets and gifs](https://github.com/danielle-han/UnityLiveProject/tree/main/FINAL%20code%20snippets%20and%20gifs)
* [Code snippets and gifs taken during development](https://github.com/danielle-han/UnityLiveProject/tree/main/code%20snippets%20and%20gifs)
* [Code snippets and gifs shown on this README](https://github.com/danielle-han/UnityLiveProject/tree/main/code%20summary%20snippets%20and%20gifs)

## Table of Contents
* [Story 1: Creating the Basic Scenes](#story1)
* [Story 2: Level Design and Player Behavior](#story2)
   * [Level Design](#leveldesign)
   * [Player Behavior](#playerbehavior)
* [Story 3: Opposition Behavior](#story3)
   * [Alien Movement](#alienmovement)
     * [Alien Group Movement](#aliengroupmovement)
     * [Lone Alien Movement](#lonealienmovement)
   * [Alien Shooting Behavior](#alienshootingbehavior)
   * [Collision Behavior](#collisionbehavior)
* [Story 4: Complete Game Play Model](#story4)
   * [UI Element Functionality](#uielement)
     * [Score and Extra Lives](#score_extralives)
     * [Showing Score in Game Over Scene](#scoreGameoverscene)
  * [Player Extra Lives](#playerextralives)
   * [Object Pooling and SetActive to False](#objectpool)
   * [Animations](#animations)
     * [Animation on Start Scene (text)](#startsceneanim)
     * [Animation of Alien Group](#aliengroupanim)
   * [Collision Behavior of Barriers](#barriercollision)
   * [Timed Inactivity](#timedinactivity)
   * [Final Game](#finalgame)
* [Story 5: Polish Game](#story5)
  * [Colored Text on Hover](#onhover)
  * [Audio](#audio)
* [All Code Snippets and Gifs](#reponav)
* [Skills Acquired](#skillsacquired)

## <a name="story1"></a>Story 1: Creating the Basic Scenes
For this story I created the basic scenes including the start scene, game play scene, and game over scene. I also created the basic framework of the start and game over scene in that I added text and buttons for navigation. I used a prefab called sceneLoader to implement navigation between scenes and added the scenes to the build index of the program so that the navigation could be functional. <br>
I also spent time during this story to plan out the project and figure out what functionalities I would need to implement for the game. For example, I took time to read up on the classic Space Invaders game and played the game to take note of the various functionalities and behaviors of the game objects.

## <a name="story2"></a>Story 2: Level Design and Player Behavior
* [Level Design](#leveldesign)
* [Player Behavior](#playerbehavior)

### <a name="leveldesign"></a>Level Design
I used primitive game objects to build out the basic layout of the game. I used basic 2d game object sprites like squares, capsules, and circles to be placeholders for the aliens (opposition), player, and other game objects. 

### <a name="playerbehavior"></a>Player Behavior
I then added player behavior such as movement and shooting behavior to the placeholder object. To implement shooting behavior, I created a placeholder object for the player bullet and attached the player bullet script. For player movement, I made use of the RigidBody component and utilized the function movePosition to move the object along the x-axis. For the player’s shooting behavior,  I created a function called Shoot() and inside this function I would instantiate the bullet object, access its RigidBody component, and add a force to it to shoot it upwards. Eventually, I updated this function to accommodate object pooling which I did in a later story. The shoot function would then be called within the Update function inside a conditional statement where Shoot() would only be called if the Space bar was pressed. <br>

Below is a snippet of the player movement script: <br>

![player movement code snippet](https://github.com/danielle-han/UnityLiveProject/blob/main/code%20summary%20snippets%20and%20gifs/story2/playermovement.png) <br>

Below is a snippet of the player shooting script: <br>

![player shooting code snippet](https://github.com/danielle-han/UnityLiveProject/blob/main/code%20summary%20snippets%20and%20gifs/story2/shootingbehavior.png) <br>

After implementing player behavior, I realized the object could move out of the screen. To address this, I create boundaries by clamping the player’s position to a maximum and minimum value to prevent the player from leaving the screen. <br>

The snippet below is the code for implementing the boundaries: <br>

![player boundaries (clamping) code snippet](https://github.com/danielle-han/UnityLiveProject/blob/main/code%20summary%20snippets%20and%20gifs/story2/playerboundaries.png) <br>

The gif below illustrates the initial player behavior that was implemented during this story. <br>

![Initial player behavior gif](https://github.com/danielle-han/UnityLiveProject/blob/main/code%20summary%20snippets%20and%20gifs/story2/prototypebullet.gif)
  
## <a name="story3"></a>Story 3: Opposition Behavior
* [Alien Movement](#alienmovement)
  * [Alien Group Movement](#aliengroupmovement)
  * [Lone Alien Movement](#lonealienmovement)
* [Alien Shooting Behavior](#alienshootingbehavior)
* [Collision Behavior](#collisionbehavior)

### <a name="alienmovement"></a>Alien Movement
#### <a name="aliengroupmovement"></a>Alien Group Movement
For the group of aliens, I implemented automatic movement for the group and used clamping to prevent it from leaving the screen. I then made sure that the group stops moving when it reached a certain y-axis value to keep it from continuously moving. For clamping, I utilized the same approach that I used for the player. For the movement itself, I used an if statement to check if the group reached a certain y value and, as long as it did not, the if else statements determining the movement of the alien group would execute. <br>

Below is a code excerpt from the alien group movement script: <br>

![alien group movement code snippet](https://github.com/danielle-han/UnityLiveProject/blob/main/code%20summary%20snippets%20and%20gifs/story3/aliengroupmovement.png) <br>

Below is a gif that illustrates the initial alien group movement as it is implemented. <br>

![alien group movement gif](https://github.com/danielle-han/UnityLiveProject/blob/main/code%20summary%20snippets%20and%20gifs/story3/aliengroupmovement.gif) 

#### <a name="lonealienmovement"></a>Lone Alien Movement
For the lone alien that moves at the top of the screen, I also implement automatic behavior where the alien would instantiate off screen from the right and move at a set speed to the left until it was out of view. The instantiation of the alien object was implemented through a function named Generate() which is very similar to the Shoot() function that instantiated bullets. The instantiation was then called in the Update function at set intervals. Below is a code snippet of the initial conditional statement that determined when the Generate() function would be called.  <br>

![lone alien movement code snippet](https://github.com/danielle-han/UnityLiveProject/blob/main/code%20summary%20snippets%20and%20gifs/story3/alien4movement.png) 

### <a name="alienshootingbehavior"></a>Alien Shooting Behavior
For the alien group, I implemented a random, automatic shooting behavior. For this I also used a conditional statement based on time inside the Update function. I set the nextFire variable to the sum of a random float from a set range and the current time. Each time the current time was greater than the nextFire value, the variable value would be set again and the Shoot() function would be called. This script was added to each alien in the alien group to implement a random, constant shooting behavior. <br>
In a later story, I eventually changed “Time.time” to “Time.timeSinceLevelLoad” on both the script for alien shooting behavior and the lone alien movement.  I realized because Time.time starts from when the program begins, it would cause issues whenever I would play the game again without stopping and restarting the program. Therefore, I updated it to Time.timeSinceLevelLoad so that the time would be restarted every time the scene loaded. The FINAL folder in the repository holds the code snippet of the updated scripts. <br>

![alien shooting code snippet](https://github.com/danielle-han/UnityLiveProject/blob/main/code%20summary%20snippets%20and%20gifs/story3/alienbulletshooting.png)

### <a name="collisionbehavior"></a>Collision Behavior
I implemented collision behavior for both the aliens and player. I ran into a problem while implementing collision behavior in that the alien bullets would collide with the aliens. This issue was solved by setting the alien bullets and aliens in separate layers and ignoring collision between the layers. For the collision behavior, I implemented OnCollisionEnter2d() as the objects had both a RigidBody2d and a collision component. Initially, before setting layers, I used a conditional statement to check for specific tags and used IgnoreCollision. I also initially destroyed the objects to remove them on collision but updated the scripts to simply set the objects as inactive. <br>

Below is a snippet of the initial script for alien collision. To see detailed or updated code snippets, check out the folders in this repository. <br>

![collision behavior code snippet](https://github.com/danielle-han/UnityLiveProject/blob/main/code%20summary%20snippets%20and%20gifs/story3/alienhit.png) <br>
 
Below is a gif illustrating the initial implementation of opposition and collision behavior. <br>

![initial implementation of opposition and collision behavior](https://github.com/danielle-han/UnityLiveProject/blob/main/code%20summary%20snippets%20and%20gifs/story3/alienshootingandcollision.gif)
  
## <a name="story4"></a>Story 4: Complete Game Play Model
* [UI Element Functionality](#uielement)
   * [Score and Extra Lives](#score_extralives)
   * [Showing Score in Game Over Scene](#scoreGameoverscene)
* [Player Extra Lives](#playerextralives)
* [Object Pooling and SetActive to False](#objectpool)
* [Animations](#animations)
   * [Animation on Start Scene (text)](#startsceneanim)
   * [Animation of Alien Group](#aliengroupanim)
* [Collision Behavior of Barriers](#barriercollision)
* [Timed Inactivity](#timedinactivity)
* [Final Game](#finalgame)

### <a name="uielement"></a>UI Element Functionality
Dynamically changing text of score and number of extra lives. 

#### <a name="score_extralives"></a>Score and Extra Lives
For the score and extra lives, I accessed each TextMeshProUGUI component holding the value for the score and number of extra lives then manipulated the text inside to reflect the right values. To do this I first had to convert the text string to an integer, add (for score) or subtract (for number of lives), and then convert the new value back to a string. <br>

Below is the initial code for dynamically changing the score text. <br>

![score text code snippet](https://github.com/danielle-han/UnityLiveProject/blob/main/code%20summary%20snippets%20and%20gifs/story4/dynamicscoring.png) <br>

Below is a gif of the initial implementation of UI element functionalities. <br>

![UI gif](https://github.com/danielle-han/UnityLiveProject/blob/main/code%20summary%20snippets%20and%20gifs/story4/INITIALdynamiclivesandscore_playerspawning.gif)

#### <a name="scoreGameoverscene"></a> Showing Score in Game Over Scene
I made use of PlayerPrefs to pass on the score value from the game scene to the game over scene. <br>

![PlayerPrefs code snippet](https://github.com/danielle-han/UnityLiveProject/blob/main/code%20summary%20snippets%20and%20gifs/story4/playerprefs.png)

### <a name="playerextralives"></a>Player Extra Lives
To implement the extra lives, I used a variable to count how many lives were used. I then used a conditional statement checking the number of extra lives used to determine whether to activate the gameObject again. If the condition was true, the gameObject would be set to active again and the number of lives text would be changed to reflect the number of extra lives left. The number indicating how many lives were used would be incremented while the number of lives left (which displays on the game) would be decremented to reflect the change. The placeholder extra life objects would also be affected to reflect the number of extra lives left. <br>

Below is a code snippet of the initial code for implementing the extra lives functionality. <br>

![extra lives code snippet](https://github.com/danielle-han/UnityLiveProject/blob/main/code%20summary%20snippets%20and%20gifs/story4/initialplayerspawning_and_dynamiclivestext.png)

### <a name="objectpool"></a>Object Pooling and SetActive to False
After some feedback from my instructor, I pooled the bullet objects and pre-instantiate a set number of bullet prefabs instead of constantly instantiating bullets every time the function was called. I also decided to change all of Destroy() to SetActive(false) to lessen the load on the program. <br>

Below is a code snippet of the player bullet pool. Here a set number of bullets is added to a list and the function GetPooledPlayerBullets() returns a bullet from the pool. <br>

![player bullet pool code snippet](https://github.com/danielle-han/UnityLiveProject/blob/main/code%20summary%20snippets%20and%20gifs/story4/playerbulletpool.png) <br>

Below is a code snippet of the updated player Shoot() function that makes use of object pooling. In this function, GetPooledPlayerBullets() is called and the bullet returned is set to active. <br>

![updated player shoot() function code snippet](https://github.com/danielle-han/UnityLiveProject/blob/main/code%20summary%20snippets%20and%20gifs/story4/updatedplayershootingfunction_forobjpooling.png)

### <a name="animations"></a>Animations
#### <a name="startsceneanim"></a>Animation on Start Scene (text)
I animated the text of the score table on the start screen. I replicated a typewriter animation using a Coroutine. Below is the initial animation of the score table. <br>

![start screen text animation gif](https://github.com/danielle-han/UnityLiveProject/blob/main/code%20summary%20snippets%20and%20gifs/story4/startscenetypewritertext.gif) 

#### <a name="aliengroupanim"></a>Animation of Alien Group 
After replacing primitive object sprites with game sprite assets, I added an animation for the sprites of the alien group. This animation was added using the given animation features in Unity.

### <a name="barriercollision"></a>Collision Behavior of Barriers 
I used a switch statement to change the sprite of the barriers on each collision.  The code snippet of the initial switch statement is below. <br>

![barrier collision code snippet](https://github.com/danielle-han/UnityLiveProject/blob/main/code%20summary%20snippets%20and%20gifs/story4/barrierCollision.png)

### <a name="timedinactivity"></a>Timed Inactivity
I included a C# script that set game objects to inactive after a period of time. This was used for the lone alien and player bullets that did not collide with anything so that they do not stay active when they leave the screen.  <br>

Below is the code for the timed inactivity. <br>

![timed inactivity code snippet](https://github.com/danielle-han/UnityLiveProject/blob/main/code%20summary%20snippets%20and%20gifs/story4/timedinactivity.png)

### <a name="finalgame"></a>Final Game
Below is the gif displaying the final game after finishing this story. <br>

![final game gif](https://github.com/danielle-han/UnityLiveProject/blob/main/code%20summary%20snippets%20and%20gifs/story4/FINALgameplay_score_shooting.gif)
  
## <a name="story5"></a>Story 5: Polish the Game
Additional features to improve user experience.
* [Colored Text on Hover](#onhover)
* [Audio](#audio)

### <a name="onhover"></a>Colored Text on Hover
On the start and game over scenes, I added a color tint transition to change the color of button text when hovered over.  <br>

Below is a gif illustrating the color change on hover. <br>

![Scene Transition](https://github.com/danielle-han/UnityLiveProject/blob/main/code%20summary%20snippets%20and%20gifs/story5/FINALstartScenetoGameTransition.gif)

### <a name="audio"></a>Audio
I also added audio components to the player bullet, player hit effect, the lone alien, and the game over scenes.

## <a name="reponav"></a>All Code Snippets and Gifs
For all code snippets and gifs see the folders in this repository. The “FINAL code snippets and gifs” folder holds screenshots and gifs for the finalized game and the “code snippets and gifs” folder holds snippets and gifs taken during the process of building the game. <br>

* [Finalized game code snippets and gifs](https://github.com/danielle-han/UnityLiveProject/tree/main/FINAL%20code%20snippets%20and%20gifs)
* [Code snippets and gifs taken during development](https://github.com/danielle-han/UnityLiveProject/tree/main/code%20summary%20snippets%20and%20gifs)

## <a name="skillsacquired"></a>Skills Acquired
1.	Through this project I became familar with Unity, Object Oriented Programming, and game object manipulation with C#.
2.	I also gained experience in collaborative work and with Agile/Scrum methodologies, DevOps, and Azure DevOps services.
3.	The Live Project also relied heavily on version control. Therefore, I also extensively practiced making pull requests, merging, committing and pushing changes, and creating branches. 

[Back to Top](#intro)
