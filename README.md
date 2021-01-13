# Virtual Reality Driving Sim
A guidebook for building and customizing a virtual reality driving simulator for use in human factors and psychology research
## How To Use This Project
We encourage any students who hope to conduct research on autonomous driving in virtual reality to use our documentation as a toolbox to get their projects started. 

You can follow the instructions below to get the simulator's core base and components up. In the folders of the repository are more specific components that you can integrate into your simulator as needed. Please contact me, Korri Lampedusa (korri.lampedusa@tufts.edu) if you have any questions about this repository or how to use it. 
## Getting Started
These instructions will walk you through how to install Microsoft Air Sim in Unity and the project files  up and running on your local machine for development and testing purposes.

### System Requirements

Download the [Unity Engine](https://unity.com/). When installed, Microsoft Air Sim comes with some sample Unity scenes and a wrapper around the AirLib library to run as a native plugin in Unity.

### Background Knowledge
This guidebook assumes that users have prior knowledge of the basics of Unity -- i.e. creating GameObjects, C# scripts, physics properties and components, UI elements, and integrating assets from the Unity Asset store. Unity has very detailed documentation, which you can check out at: https://docs.unity3d.com/Manual/index.html

### Installing Microsoft AirSim
The github documentation for [AirSim](https://github.com/microsoft/AirSim/blob/master/docs/Unity.md) includes intructions for installing the Car simulator but these instructions miss several steps. Thus we have included a more detailed set of instructions here detailing some common errors/ mistakes but many of the steps are paraphrased from the original documentation.

#### Build AirSim
* Install Visual Studios 2019.
	* During installation, select: "Desktop Development with C++", and "Windows 10 SDK 10.0.18362" (or most current match)
* Once installed, open the `x64 Native Tools Command Prompt for VS 2019` after Air Sim has downloaded.
	* This is different from the Windows Command Prompt.
* First, you need to change to your computer's root directory using `cd / .`. This step is necessary so that you have write permission to clone the repository. 
* Make a new folder for these files on your computer using `mkdir YourFoldersName`.
* Change into that folder using `cd YourFoldersName`
* Now you will clone the Airsim repository to your local machine to the folder you just created using `git clone https://github.com/Microsoft/AirSim.git`
	* If you are having issues using git commands, you may need to install git on your local machine. 
	* If you are still encountering issues cloning the repository, you can go to advanced system settings and manually set your Path to point at your git 			   installation.  Inctructions for this can he found [here](https://stackoverflow.com/questions/4492979/git-is-not-recognized-as-an-internal-or-external-command)


* Once the repo is successfully cloned, go to the Air Sim directory using `cd AirSim`
* Run `build.cmd` from the command line
* It is possible that your build will fail and ask that you: `install CMake by pressing any key`. 
	* Press any key, then while going through the CMake setup wizard, Make sure you choose 'add to the path for this user' on setup (it is not the default choice)
	* For resolving other CMake issues that might arise depending on your computer's advanced system settings, you can read 
	[this thread](https://github.com/microsoft/AirSim/issues/755)
* Once you resolve these issues related to CMake, it is possible your build will fail again due to a warning that is interpreted as an error. [Here](https://github.com/microsoft/AirSim/issues/3136 ) is the solution and explanation of this error. Note: To access the XML file this solution references, just right click on that file and open with Notepad.
* The Build should successfully run now.

#### Build Unity Project
* Go inside the AirSim\Unity directory: `cd Unity`.
* Build the unity project by typing into the command line: `build.cmd`

#### Downloading Windridge City
* After the Unity project is built, go to open a new Unity project and create a scene
* Go to the Asset Store and search "Windridge City" and download the asset of the same name
* After downloading there should be a folder in your scene titled `Windridge City` with a subfolder `Scenes` that holds a scene titled `Windridge City Demo`. Double click on this scene to launch
* Upon opening this scene and trying to run it, a whole host of errors will pop up. The reason for this is the correct postprocessing package is not installed. Go to the `Window` tab in Unity and click on package manager in the drop down menu.
* Go to the Postprocessing tab and select `Install` for the most recent version of the postprocessing script. If the Postprocessing tab is not appearing, switch the view from `In Project` to `All`
* Air Sim should be fully set up after this point

#### Possible Issues and Solutions
* The warning `Lighting data asset 'LightingData' inconsistent. Please use Generate Lighting to rebuild the lighting data` is appearing:
	* Ensure that in the `Windows > Postprocessing` tab that the postprocessing script version 2.0 or higher is installed. Restart your game if you just updated the script and this error continues to appear.
* Are all the roads appearing streaked with white?
	* Go to `Assets> NatureManufacture Assets - Trials Not Full Resolution> EasyRoads-HD_Add_On > RoadMaerials > Asphalt` and there will be 5 road materials present
	* Click on any of the road materials and in the inspector, navigate down to the details Albedo Map and adjust the `Main Road Detail Albedo` value until the white patches dissappear.



