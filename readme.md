# COMP3111 Project - Tower Defense
Created by: Dr. Kevin Wang (kevinw@cse.ust.hk)

## Project Problem Statement and Activities
 
 ### [Project Sign Up](https://docs.google.com/spreadsheets/d/1fGQYkAsdawLWlxSNlFxJr192ZFOIowbVIUD1EoVWuYc/edit#gid=0)
 
 
 > **Activity 1 Due (2%): ~~14-10-2019 (Wk 7 Mon)~~ 21-10-2019 (Wk 8 Mon) 20:00**
 > Submission details will be provided on Canvas
 >
 > **Activity 2 Due (28%): 17-11-2019 (Wk 12 Mon)**
 > Submission details will be provided at Canvas - (Design Pattern and Java Doc will be due on 20-11-2019)
 
 ## Import Updates
 
 ## Introduction
 
 You are going to form a team of three to work on a project. The project is about writing a computer game tower defense (TD). Every fraction of second a monster will be generated at the starting position. These monsters will move towards the end-zone.  Once a monster reaches the end zone the game ends and the player lose the game. To avoid the monster reaching the end-zone, the player can use the resources earned in the game to build different types of tower that attacks and destroys monsters. You are given a skeleton code written in Java 11 that allow you to build one tower on the map and generate one monster. This skeleton does not really do anything and you may actually change everything you are given in the project (including not using the skeleton code at all). 
  
You are advised to read this document carefully and ask your question on Piazza (access via Canvas). We will answer your questions promptly.
 
    
 There are 3 tasks for each group to complete. Each student should complete one of the tasks. For students enrolled in COMP3111H, there is some additional requirements on the task that you have subscribed. Each task has a full mark of 15 and it be converted to a maximum of 16 points of your course total (`mark / 15 * 16`). For COMP3111H students the maximum possible score will be 25, however, it will be converted to a maximum of 16 points of your course total (`mark / 25 * 16`). Thus, the maximum possible marks for regular task and H task are the same. 

The task specifies what should be done but there are still a lot of details unspecified. We deliberately not specify those details in the implementation and allow students to fill the missing gaps. However, to make sure the game would make sense and meet our expectation, we define a set of game physics that your team must follow. If your team fail to follow those physics marks will be deducted. At any time if you and your teamate wish to clarify with a particular task requirement, you should ask on Piazza. TAs who responsible for grading will only read the clarification written on Piazza.

About group formation, you are allowed to team up with students enrolled in different sessions. **However H class students can only team up with H-class students (L1 or L2).**  

Apart from the implementation of the tasks, there are some other requirements on the project such as documentation, testing, design patterns. They will be stated after the task specification.

Noted that the some tasks are in a hierarchy structure. No point will be awarded if the parent task is not completed. Points are given in all-or-nothing fashion. 
 
 ## System Requirements
 
 ### Game Physics
 
 Regardless how you implement the game, there are some ground rules that need to follow. If your task has violated these physics, penalty may be applied to individual or to the whole group. So please take extra attention to these rules.
 * A tower can only be placed on one grid, not crossing the border. 
 * A monster is modeled as a point which should be roughly the center of its icon/grid. In other words, a monster has a size of 1px by 1px.
 * A monster is always moving from a grid to an adjacent grid either horizontally or vertically.
 * The game must not allow a player to build a tower if the player does not have enough resource to build it.
 * When a monster is killed it must be removed from the arena, a certain amount of resource will be given to the player.
 * Each grid can contain at most one tower. When it contains a tower, it cannot contain any monster.
 * No tower shall be able to move. 
 * All distance used in the game should be referred as Euclidean distance, in pixels (px). 
 * The width and height of the Arena is 480 px-by-480 px. 
 * All operations by the player must be done by mouse.
 * A tower must have at least the following information: attack power, building cost, shooting range. 
 * A tower cannot attack a monster that is outside its shooting range. When we judge a monster is inside a tower's shooting range, the following distance will be used: the Euclidean distance between the center of the grid of where the tower is built and the center of the monster.
 * The health point (HP) of a monster will be deducted by the attack power of the tower attacking it. When HP is less than or equal to zero a monster is killed. 
 * When there are multiple possible monster a tower can shoot (in range), it should always choose a monster that is nearest to up-left corner of the end-zone ((440, 0) in our demo).
 * It is allowed that multiple towers shoot at a monster at the same time even through only one tower is needed to kill it. This is likely to happen. 

#### Rules applies to COMP3111 groups only. 
 * There are two different colors of grids - green or white. A green grid can only contain a tower. A white grid can only contain monsters. Both kinds of grids may cannot change its color in the middle of the game.
 * A white grid can contain any number of monsters.
 * The game is a turn-based game. In each turn, a player will need to click the button `Next Frame` to run. Then each monster will move certain distance, according to its attributes and status. Each tower may or may not fire, depends on its individual position, attributes, and status etc. In between two clicks of `Next Frame` the player may also allowed to build or destroy towers, whenever resources are enough.
 * When the word `time` is every used in the task description (e.g. 2.iii) , it refers to one *frame* (a click of `Next Frame`) or several frames. 


#### Rules applies to COMP3111-H groups only. 
 * A monster will never move toward a grid with a tower. If a monster is already on its way to a new grid and a part of the monster body is already insider the grid, no tower will be allowed to be built on this new grid. 
 * After building a tower, all monsters on the map should have at least one valid path move toward the end-zone. Thus, the game must not allow a player to build a tower to trap a monster. 
 * Each grid can contain any number of monsters as long as it does not contain a tower.
 * The game is a time-based game. The button `Next Frame` would NOT be tested in grading. It will be served as a debug button for your own interest. There are two methods to start the game: by clicking `Simulate` or `Play`. In either mode monsters will be automatically generated and the monsters will move towards the end-zone, towers will automatically fire if any monsters are in its shooting distance. In `simulate` mode, player is only allowed to build tower before the simulate button is clicked. Once the button is clicked, the player will no be clicking any button until the game is over. In `play` mode, the player is allowed to build or to upgrade tower when the game is running.
 
### Tasks (16 points of project Total)
 
#### Regular Individual-Task - applies to both 3111 and 3111H students
1. Arena Building (15)
    1. Indicate the grid that a monster show up and the grid representing end-zone with png images. 
    The image must shall be shown at the back when there is a monster on the grid. Create/choose your own image. (1)
    1. Allow all types of towers to be built on all green grids using drag and drop gesture. (1)
        1. When a tower is built, an image of the tower will be placed on the grid. Use the png files 
        provided under `src\main\resources`. (1)
        1. A fixed amount of resource (e.g. money, or you create your own set of resources.) is deducted 
        and correctly display the remaining amount of resource on GUI screen after building
        the tower. (1)
        1. When the mouse pointer is moved over a built tower, all information related to the 
        tower must be displayed on the graphic interface (`System.out.println` is not acceptable)) (1)
            1. Furthermore, the pixels of the area that are inside the tower's range are shaded (you might use a circle UI). (1)
                1. Furthermore, when the mouse is moved away from the tower, the shaded area will be restored (you are not allowed to dismiss the information/shaded pixel by clicking button, e.g. click a message box). (1)
        1. When there is not enough resource to build a tower, the program should prompt a dialog box to warn the player (1)
        1. When a tower is clicked, the player will be provided with two options: `destroy the tower` and `upgrade`. (1)
            1. Furthermore, when `destroy the tower` is selected, the tower will be destroyed. (1)
            1. Furthermore, when `upgrade` is selected, and in case there is enough resource (you can determine the resources needed) to upgrade, it will invoke the function that corresponding to 
            upgrading the tower and a line `XXX tower is being upgraded` is printed on the console. (1)
                1. Furthermore, in case there isn't enough resource to upgrade the tower, the upgrade will be aborted and a line `not enough resource to upgrade XXX tower` is printed on the console. (1)
    1.  Logging the following information using `System.out.println`:
        1. When a monster is generated. Log its type and HP in the format `<type>:<HP> generated` (1)
        1. When a monster is attacked. Log the type and position tower attacks it and the position of the monster in the format `<tower_type>@(<x>.<y>) -> <monster_type>@(<x>, <y>)` (1)
            1. Furthermore, represent the attack in the GUI so that the monster and the tower involved can be visually identified without reading the log. (1)
1.  Towers (15)
    1.  All towers built in the arena will shoot a monster automatically which is inside its range (unless all towers are impossible to attack, e.g. out of range, in cool down etc). (1)      
    1.  Implement Basic Tower that has a shooting range [0,65] pixels. You can decide the attack power and other parameters of the tower. (1)
        1. Implement the upgrade function of Basic Tower that increase the attack power of the basic Tower. (1)
    1.  Implement Ice Tower that will make monster move slower for a period of time (Take a human noticeable longer time to move without making other monster move slower). You can determine other attributes of Ice Tower. (1)
        1. Implement the upgrade function of Ice Tower that increase the duration of the monster being slowed. (1)
    1.  Implement Catapult that:
        1. it throws a stone (attacks) to a coordinate less than 150 px but more than 50 px away from the center of the Catapult. (1)
        1. All monsters placed at the radius of 25px of where the stone drop receive damage. (2)
        1. After a stone is thrown, the Catapult take some times to reload the stone (cold down). During that period of time the Catapult will not be able to throw a stone again. (1)
            1. Furthermore, implement the upgrade function of Catapult that the reload time/cold down time is shorten. (1)
    1.  Implement Laser Tower that:
        1. it consumes some resources to attack a monster. (1)
        1. draw a line from the center to the tower to the monster and extend beyond until it reach the edge of the Arena. (2)
            1. Furthermore, all monsters on the line or within 3px away from the line will receive damage. (1)
        1. Implement the upgrade function of Laser Tower that increase attack power of the tower. (1)   
    1. *noted: you are allowed to determine the parameters and cost of your towers when it is not specified. For instance, we did not say if an Ice tower will give damage or not and you can decide that.*
1. Monsters (15)
    1.  In every fixed period of time, one or more monsters will be generated in the arena from a fixed grid that the monster shows up. (2)
        1. Furthermore, along the time elapsed the *stronger* the monster will be generated so that the difficulty of the game increase. *Stronger* may refer to more HP, moving faster, or any factors that make the game difficult to play. You can make your own definition of *stronger*. (1)
    1.  Monsters on the arena will move towards the end-zone automatically. (1)
        1. Furthermore, if no tower is built, the monster will be successfully reach the end-zone and cause the game over (player lose). A single line `Gameover` will be printed to console. (1)
            1. Furthermore, if the game is over, both monster generation and tower shooting should stop and a dialog box will pop up to notify the game is over (1)
    1.  Represent a monster with png images (`fox.png`, `unicorn.png`, `penguin.png`) provided under `src\main\resources`. (1)
        1. Furthermore, when a monster is killed (HP reach 0), its image will be replaced by `collision.png`. (1)
            1. Furthermore, the dead monster will be removed from the arena automatically. (1)
    1.  When a mouse pointer moves over a monster, the HP of the monster will be shown on the graphical interface. (1)
        1. Furthermore, when the mouse pointer moves away from the monster, the HP information will be dismissed. (1)
    1.  Implements three types of monsters: Fox, Unicorn, Penguin such that:
        1. Fox move fastest. (1)
        1. Unicorn has more HP than other monsters. (1)
        1. Penguin has can replenish some HP (but not more than its initial value) each time it moves. (2)

#### H Individual-Task - applies to 3111H students only - (5%)
1.  Arena
    1. Allow player to build towers in all grids unless it violates the rules stipulated in the Game Physics - Rules for H task. (1)
    1. Implement the button `Simulate` according to the game physics. (2)
        1. Furthermore, implement the button `Play` according to the game physics. (2)
1.  Tower
    1. Catapult attacks algorithm. Instead of throwing a stone to a particular monster, the Catapult will throw a stone
    to a coordinate such that 
        1. among all monsters falls into the attack range plus 25px (the stone radius), the one monster which
    is nearest to the end-zone will be attacked; and (1)
        1. the stone should thrown to the coordinate that hits most monsters; (2)
        1. Rule for tie-breaking: If there are two monsters that are both considered nearest 
        to the end-zone, the stone will be thrown towards the one that hits more monsters. If the same number of monsters
        are hit by the stone, choose any monster you wish. (1)
            1. Create a test case in JUnit to show your algorithm. (1)
        1. *Note: a stone can be thrown to a grid that contains a tower if it make sense. The tower will not be destroy because of that.*
1.  Monster
    1. All monster are able to walk towards the end-zone with a shortest path (choose any path if there are two shortest paths). (1)
        1. Furthermore, Fox is a very wise monster that will not simply walk a shortest path. Fox will try to 
        follow a path that receives a minimum number of attacks from towers by assuming that there is no other monster in Arena. (2)
	1. Create a test case in JUnit to show your algorithm. (1)

#### H Group-Task - applies to 3111H students only - (5%)
1.    Adopt the following technologies into your project. 
	1. Use Java Persistence API or Hibernate Framework to connect to a small database that stores your game data (attributes of Towers/Monsters); (2.5%)
	1. Use Java spring framework that allows the game be played in different machines while a server records the top 10 highest scores; (2.5%) 

* Note: no implementation group task for comp3111 student.
 ---
 
 ## Technical Requirement
 
 1. The program must use Java 10 or above. 
 1. The project must use Gradle to manage. You might change the `build.gradle`.
 1. The program must use JavaFX as its only GUI framework. Using Swing or AWT without prior permission will incur penalty.
 1. You may choose your own IDE. We recommend Eclipse IDE.
 1. JUnit 4.12 as your testing suite.
 1. Jacoco as your test coverage measurement.
 1. A Private GitHub repository for source control
 	1.	students can apply for [GitHub Education](https://education.github.com/) or a regular Github account. 
 	1.	In your private repository setting page, add your team members and all TA as collaborators. The TA account is `comp3111ta`.
 
 ---
 
 ## Team Requirements
 
 1.	Cross-section team forming is allowed (i.e. L1 students can form a team with L2 students)
 1.	Each team MUST be formed by 3 students enrolled in COMP3111 or COMP3111H.
 	1. Team of 1/2/4/5/6/.. is never allowed.
 	1. The teaching team will randomly assign the ungrouped students. Mathematically we might have one or two group of two.  
 1. Each team member is expected to implement one task from the system requirements.
 	1. No two students in the same group can implement the same task. Students are expected to divide the workload by themselves.
 	1. The member implementing the task is also required to manage the Git commit log messages, testing, debugging, and documentation of the task.
 	1. Two developers may need to work on the same Java method concurrently. Team discussion meetings and version control using Git are essential to minimize conflicts during the software development process.
 
 ---
 
# Activities to submit
 
## Activity 1 - System Requirement Specification (2%)
 
Based on the above project requirements, prepare and submit
1.	Team work
 	1. A use-case specification of all tasks (2%)
 
## Activity 2 - Software Implementation and Testing (28%)
1. Team work - Submit to canvas
 	1. At least 3 meeting minutes. (0.5%) (submitted at the end of this course)
 	1. A Gantt chart and a burn down chart. (0.5%)
1. Team work but mark individually - Submit one copy per group to Github
 	1. A `readme.md` file stating the name of team members and their tasks assigned.
 	1. A running program and the source code. (16%)
 	1. Unit testing of your implemented tasks. (100% pass - 1%; 0% otherwise) 
 		* Even if you are failed to implement all tasks, the unit testing is still required.
 	1. Coverage test (>70% branch coverage- 2% ; 50-70% branch coverage - 0.5%; 0% otherwise;)
 		* Even if you are failed to implement all tasks, the coverage test is still required.
 	1. Git commit log at GitHub. At least three "non-trivial" commits and one "non-trivial" pull request (per student) (1%)
 	1. *Notes: In case full mark is not given to the group, marks will be given to student individually based on the completion of their own tasks.*
1.  Team work - Submit one copy per group to Canvas (+3 Day due after the Code) 
	1. Design Pattern Document (6%) - A document stating at least three design patterns that have been used in project. A clear justification shall be given to each of the design pattern stated including what design goal has been achieved, a class diagram of that design pattern (with relevant methods/attributes only). Higher marks are given to correct use of pattern. Marks could be deducted if certain obvious design pattern is missing or unsuitable design patterns is misused.
 	1. Documenting your implemented features using JavaDoc (Full mark 1%: -0.25% for each missing argument, return value, exception, class description; same mark for all members)
 		* If a function is responsible by more than one student, all of them will receive the penalty.

 
 We expect most of the students will finish the project with reasonable efforts. They will most likely receive full marks.
 
 * No bonus. 
 * No late submit.
 * Testing on JavaFX may require additional framework (TestFX) which will not be covered in the course. It is optional for you to use it or not. 
 * Check the Issue page for and FAQ questions.
 
 ---
 # Grading process


## For 3111 students
 
No live demo is required/allowed.  The TA will perform the following in a lab machine.
 ```
 git clone <YOUR_URL> .
 git log # to make sure the last update is before the project due. 
 gradlew build
 gradlew jacocoTestReport
 gradlew javadoc
 gradlew run
 ```
 You will be invited to appeal at a later time if your code does not work.

## For 3111H students

No live demo is required. You will need to teach the TA to conduct a grading process in a lab machine if you need to starts a local database server. Write your grading process in your readme.md. You may also ask for a live demo. Make an appointment with the TA. 


## Note

For both 3111 and 3111H students, we will give you a preliminary mark after we have reviewed your project. You can appeal your marks in the appeal session. 
 


