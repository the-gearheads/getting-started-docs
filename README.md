## Getting Started

### Vocab
Firstly, these are some basic terms that may be nice to know:  

**FRC** - FIRST Robotics Competition, the one we participate in  
**WPILib** - Main library used for developing FRC bots  
**RoboRIO** - The "computer" or controller we connect motors to that executes our robot code  
**Falon 500** - The motors that we use. They have a built in Talon SRX motor controller which communicates over CAN.  
**CAN Bus** - The protocol used to transmit data throughout the robot. It uses 2 wires.  
**NEO** - Another motor that we use. Weaker than the Falons. You need to use them with a motor controller like the **REV SparkMAX**  
**NEO 550** - A significantly sized down version of the NEO, good for smaller applications  

**NetworkTables** - A protocol between the robot and the driver computer that allows for setting variables over the network. Used for telemetry and setting other options usually.  
**Dashboard** - The piece of software that we use to interface with NetworkTables variables on the driver's computer  
**Driver Station** - Refers either to the computer that the driver uses, or the software **FRC Driver Station**, which communicates with the RoboRIO, lets you set the operation mode, and takes in controller input, to send to the robot.  

**Disabled Mode** - Self-explanatory, the robot cannot move or do anything  
**Teleop Mode** - For the teleop part of the competition where a human drives the robot.  
**Auton Mode** - The part of the competition where the robot drives itself  

**Odometry** - Measuring how many times each wheel has rotated to estimate our position on the field  

**Command Based** - A framework for writing robot code that primarily involves commands and subsystems  
**Subsystem** - In command based, a section of the robot that handles a function, for example, the drivetrain, or the shooter.  
**Command** - In command based, a certain command, or task, that the robot is programmed to do. For instance, ArcadeDrive, or MoveToBall would be decent command names.  

There are some more definitions at https://docs.wpilib.org/en/stable/docs/software/frc-glossary.html

### Installing tools

##### Quick Guide
Here's the condensed version:
1. Install Visual Studio Code
2. Install the following extensions in VSCode:
   - [WPILib](https://marketplace.visualstudio.com/items?itemName=wpilibsuite.vscode-wpilib)
   - [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)
   - [Java Extension Pack](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack )
4. Install Git for Windows, set the default editor in the installer to VSCode
5. Install the FRC Game Tools
6. Install the [x64 JDK](https://www.oracle.com/java/technologies/downloads/#jdk19-windows)

#### Why we use Git
Git is a source control manager, which means that it manages source code. It keep track of code across various branches, and keep track of every change you make in a unit called a commit. Each commit contains a set of changes that you're making, and they're kept across branches, which, like a tree, diverge from each other, taking different paths, and containing different commits. 

The reason why git needs a default text editor is that git uses the text editor to resolve merge conflicts, which are when you're merging 2 branches and they have conflicting changes (e.g. 2 commits edit the same line).

#### Why we're using the other tools
- We use VSCode as our primary code editor primarily becuase WPILib is designed to use it, and it's quite nice to use (though it is possible to use IntelliJ if that's your preference)
- The VSCode extensions simply make development easier. GitLens improves VSCode's git integration so you hopefully don't have to resort to the terminal/command line as much (but you should still learn it!). 
- The WPILib extension has a lot of useful shortcuts for WPILib specific things, and sets up autocomplete for the Java extension pack. accessible mainly through the command palette (Ctrl+Shift+P to open)
- FRC Game Tools contains the FRC Driver Station we use to drive the robot, it's essential. 

### Downloading and building a project
Before we get to making our own project, let's first take our shot at building an existing one, https://github.com/the-gearheads/2022Robot. This is our 2022 robot code. So, if I'm going to be honest, with our currently installed tools, I don't know if there's a way to clone (download) a git repository without using the command line. So, we'll just use that for now. 

#### Mini Windows Command Line Tutorial
1. To start, open the start menu and type `cmd` and hit enter.
2. A window will open. The line at the bottom is where you type your command, and what's already on the line is called the prompt. Before the `>` is the current path that you're in. You can imagine this as being the same as going into folders normally in file explorer. 
3. To list the files in the folder you're in, type `dir` and press enter to execute it. It will show you which are folders and which are files with the `<DIR>` part. Note that most commands will also take some arguments (options) after their command name. For instance, `dir` takes an argument `/w`, that lists the files in a more compact fashion. The final command would look like `dir /w`
4. To change your folder, do `cd foldername`, replacing the folder name. If your folder contains spaces, you should surround it with quotation marks (""). The name of one folder up is always called `..`, so to go back a folder, do `cd ..`
5. If there is an exe or bat file in the folder you're in, you can run it just by typing it's name, like this: `gradlew.bat`. 

#### Actually cloning the project
We will place the project in the Documents folder. 
1. Open cmd, by opening the start menu, and typing `cmd`
2. `cd Documents`
3. `git clone https://github.com/the-gearheads/2022Robot`. Git will create a new folder in Documents called 2022Robot that contains the code.
4. If you wish to, you can go into the folder with `cd 2022Robot`

#### Opening it in Visual Studio Code
1. Open Visual Studio Code
2. Go to File -> Open Folder
3. Select the 2022Robot folder in your documents. 
4. Wait for it to load. 
5. Press Ctrl+Shift+P to open the Command Pallete, which is the easiest way to access most of VSCode's functions. 
6. Type `Build Robot Code` and hit enter to select the `WPILib: Build Robot Code` option. The code should build without error (hopefully). 

#### Deploying Code on a Real RoboRIO
This is fairly simple: Run the `WPILib: Deploy Robot Code` option, after first connecting to the robot's wifi network. They are named `1189_NOTAVIRUS` and `1189_2008Robot` currently. Make sure the RoboRIO is on and ready. 

#### Running the Code in a Simulation
WPILib supports running code in a simulation, so that you do not need to always have a real robot on hand. The 2022Robot code you have cloned does not have code written for proper simulation support, but the other 22.5Robot project in our the-gearheads Github organization does. To run simulated code, select the `WPILib: Simulate Robot Code` option. It will open an interface that looks similar to the dashboard called glass, where you can set keybinds, set the current mode, and many other things. 

#### Addendum:  Building and deploying from the command line
Gradle, the build system used for WPILib projects, is invoked by doing `gradlew` on Windows, and `./gradlew` on Linux, in the root project folder. Gradlew takes in an argument, which is the task to run. There are three tasks that you need to know about:

- `build` - Builds the project  
- `deploy` - Deploys the project to a roborio  
- `tasks` - Lists all tasks  

For instance, if I wanted to build the project, I would do:  
- Windows: `gradlew build`
- Linux: `./gradlew build`

### Next Steps
Please read a lot of the [WPILib docs](https://docs.wpilib.org/en/stable/index.html)! They have a lot of useful information, especially the articles about command-based. Maybe learn how to install the CTRE Phoenix libraries and write your own basic robot code in a new project to familiarize yourself, anything goes. Also, other robot code makes a great reference. We currently have https://github.com/the-gearheads/2022Robot, our somewhat disorganized competition code, and 2 offseason rewrites that only really contain drivetrain code, https://github.com/the-gearheads/1189-Common and https://github.com/the-gearheads/22.5Robot. 
