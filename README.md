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
Our simulator toolbox leverages Microsoft's open source project AirSim. The github documentation for [AirSim](https://github.com/microsoft/AirSim/blob/master/docs/Unity.md) includes intructions for installing the Car simulator but these instructions miss several steps. Thus we have included a more detailed set of instructions here detailing some common errors/ mistakes but many of the steps are paraphrased from the original documentation.

#### Build AirSim
* Install Visual Studios 2019.
	* During installation, select: "Desktop Development with C++", and "Windows 10 SDK 10.0.18362" (or most current match)
* Once installed, open the `x64 Native Tools Command Prompt for VS 2019` after Air Sim has downloaded.
	* This is different from the Windows Command Prompt.
* First, you need to change to your computer's root directory using `cd / .`. This step is necessary so that you have write permission to clone the repository. 
* Make a new folder for these files on your computer using `mkdir YourFoldersName`
* Change into that folder using `cd YourFoldersName`
* Now you will clone the AirSim repository to your local machine to the folder you just created using `git clone https://github.com/Microsoft/AirSim.git`
	* If you are having issues using git commands, you may need to install git on your local machine. 
	* If you are still encountering issues cloning the repository, you can go to advanced system settings and manually set your path to point at your git 			   installation.  Inctructions for this can be found [here](https://stackoverflow.com/questions/4492979/git-is-not-recognized-as-an-internal-or-external-command)


* Once the repo is successfully cloned, go to the AirSim directory using `cd AirSim`
* Run `build.cmd` from the command line
* It is possible that your build will fail and ask that you: `install CMake by pressing any key`. 
	* Press any key, then while going through the CMake setup wizard, Make sure you choose 'add to the path for this user' on setup (it is not the default choice)
	* For resolving other CMake issues that might arise depending on your computer's system settings at the time of installation, you can read 
	[this thread](https://github.com/microsoft/AirSim/issues/755)
* Once you resolve these issues related to CMake, it is possible your build will fail again due to a warning that is interpreted as an error. [Here](https://github.com/microsoft/AirSim/issues/3136 ) is the solution and explanation of this error. Note: To access the XML file this solution references, just right click on that file and open with Notepad.
* The Build should successfully run now.

### Building Unity Project File 
#### Build Unity Project
* Go inside the AirSim\Unity directory: `cd Unity`.
* Build the unity project by typing into the command line: `build.cmd`

#### Downloading Windridge City
* After the Unity project is built, go to open a new Unity project and create a scene
* Go to the Asset Store and search "Unity Standard Assets" and download the asset of the same name. Once it is downloaded, Import it to your scene. 
	* Assuming you are using a Unity Editor that is 2019 or later, you will likely get a compiler error about the file `public GUIText camSwitch...`. This can be resolved with a change to 2 lines of code in that file that there is documentation for [here](https://answers.unity.com/questions/1638555/guitexture-adn-guitext-are-obsolete-standard-asset.html)
* Go to the Asset Store and search "Windridge City" and download the asset of the same name.  Once it is downloaded, Import it to your scene. 
* After importing, there should be a folder in your scene titled `Windridge City` with a subfolder `Scenes` that holds a scene titled `Windridge City Demo`. Double click on this scene to launch
* Upon opening this scene and trying to run it, a whole host of errors will pop up. The reason for this is the correct postprocessing package is not installed. Go to the `Window` tab in Unity and click on package manager in the drop down menu.
* Go to the Postprocessing tab and select `Install` for the most recent version of the postprocessing script. If the Postprocessing tab is not appearing, switch the view from `In Project` to `All`
* Air Sim should be fully set up after this point

#### Possible Issues and Solutions
* The warning `Lighting data asset 'LightingData' inconsistent. Please use Generate Lighting to rebuild the lighting data` is appearing:
	* Ensure that in the `Windows > Postprocessing` tab that the postprocessing script version 2.0 or higher is installed. Restart your game if you just updated the script and this error continues to appear.
* Are all the roads appearing streaked with white?
	* Go to `Assets> NatureManufacture Assets - Trials Not Full Resolution> EasyRoads-HD_Add_On > RoadMaerials > Asphalt` and there will be 5 road materials present
	* Click on any of the road materials and in the inspector, navigate down to the details Albedo Map and adjust the `Main Road Detail Albedo` value until the white patches dissappear.
	
#### Converting the Standard 3D Project to a Virtual Reality Compatible Project
* Once you have a file with the Windridge City asset properly built and running, there are a couple of steps necessary before your project will be compatible with a VR headset.
* First, go to `Edit > Project Settings > XR Plug-In Management`, and check off `Initialize XR on Setup`. This step is what XR-enables the project.
* Within that same tab, check off `Oculus` so that the project works with your Rift S. 
* Now, you will need to go to the project's hierarchy, and create a new camera game object in the hierarchy. 
* Change the tag of that camera to be the main camera in the scene. 
* Right click on that camera, and go to `XR > Make XR Rig`, selecting 'Make XR Rig' so that this camera is comverted to one that will automatically adopt all of the backend functionality to be controlled by the VR headset's positional data. 
* Delete the original main camera object 
* XR capabilities should now work! To test this, ensure your Rift S is connected and initialized within the Oculus desktop app, then just press play in the Unity editor.

## Authors
*As of 1/12/2020*

This Repository is a forked repository of Priya Misner's original [Virtual Reality Driving Sim](https://github.com/p-misner/VirtualRealityDrivingSim) Documentation. Priya Misner, Julie Yeung, Stephanie Bentley, Caleb Jeanniton and myself were contributors to that original branch. This branch is appended with updated with my recent contributions. My current team members, Julie Yeung, Stephanie Bentley, Caleb Jeanniton, Barrett Roman, and Ioana Lupascu will be future contributers of this repository as we continue the work Spring 2021.
