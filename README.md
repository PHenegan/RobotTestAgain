# FRCBase

A blank FRC GradleRIO project for internal use by Team 555. The only real improvements of this quickstart over GradleRIO is having a libs folder which this project automatically reads from. We've also done some tweaks to make set up easier, including this step-by-step documentation.

## Table of Contents
1. [Setting up a new project](#setting-up-a-new-project)
2. [Migrating an existing project](#migrating-an-existing-project)
3. [IntelliJ set up](#intellij-set-up)
4. [Eclipse set up](#eclipse-set-up)
5. [Updating GradleRIO](#updating-gradlerio)
6. [GradleRIO command reference](#gradlerio-command-reference)

## Setting up a new project
1. Download the latest release and unzip it.
2. Change the name of the folder to match the desired name of your project.

That's all you have to do if your team number is 555. If it's not, follow these steps:

3. Open `build.gradle` in a text editor. Change 555 in the `TEAM` variable and the `ROBOT_CLASS` variable to what your team number is.
4. In the source files, refactor the package team number to your own.

Now you can set up your IDE.

## Migrating an existing project
1. Download the latest release and unzip it.
2. Change the name of the folder to match the desired name of your project.
3. Delete the source folder in the base.
4. Open your current project in file explorer.
5. Copy over your project sources (the contents of the `src` folder) to the new base. Make sure all the java files are in `src/main/java` if they are not. You can also copy over any text files your project may have to the root directory. *Do not copy libraries yet. Do not copy any previous Gradle or IDE files.*
6. Copy any jar libraries you have to the `libs` folder.
7. Open `build.gradle` in a text editor. If your team number is not 555, change the `TEAM` variable to your team number.
8. In the `ROBOT_CLASS` variable, enter the location of your robot's main class.

Now you can set up your IDE.

## IntelliJ set up
1. Make sure IntelliJ is closed if it is not already, then clone the project.
2. Double click `setup_intellij.bat`. This will generate files all the IntelliJ specific files for the project. Alternatively, you can run `./gradlew idea` in the project directory on either Powershell or a Linux shell.
3. Double click the `FRCBase.ipr` file which was just generated. IntelliJ should open the project. Sometimes `ipr` files may not be associated with IntelliJ. If this is the case, make sure to use the Windows open file menu to open the file with the IntelliJ exe. If this does not work, you can also open IntelliJ and open the project in the open project menu.
4. Once IntelliJ is opened, a tooltip should open in the bottom right which says `Unlinked gradle project?`. Click `Import gradle project`.
5. Make sure `Use default gradle wrapper` is selected, then click `Finish`.
6. From the menu bar, click View > Tool Windows > Project. (Or press Alt+1).

Now your project should be set up. It's recommended you add some build tasks to IntelliJ to make building easy:

7. From the menu bar, click Run > Edit Configurations.

From here we'll repeat a couple steps to add all the build tasks we'd reasonably need:

8. Click + > Gradle.
9. Fill in Name: `Build`.
10. Fill in Gradle project by clicking on the folder icon and selecting `FRCBase`.
11. Fill in Tasks: `build`.

That's all you need to add a build task. You should repeat steps 8-11 for the following build tasks as well (replacing name and tasks with the appropriate name):
- Deploy (deploy)
- Smart Dashboard (smartDashboard)
- Offline deploy (build deploy --offline)

Once you've finished, these should all appear in the run drop down menu on the toolbar.

## Eclipse set up
1. Make sure Eclipse is closed if it is not already, then clone the project. This does not have to be in your Eclipse workspace.
2. Double click `setup_eclipse.bat`. This will generate files all the Eclipse specific files for the project. Alternatively, you can run `./gradlew eclipse` in the project directory on either Powershell or a Linux shell.
3. Open Eclipse.
4. From the menu bar, click File > Import.
5. From the drop-down menu, expand Gradle and click `Existing Gradle Projects`.
6. Click through the intro screen.
7. For the project root directory, navigate to where you cloned the project. Then click Finish.

Now your project should be set up. It's recommended you add some build tasks to Eclipse to make building easy. (Eclipse saves build tasks across projects so you can skip this if you've done it before):

8. From the menu bar, click Run > Run Configurations.

From here we'll repeat a couple steps to add all the build tasks we'd reasonably need:

9. Click `Gradle Project` in the menu, and then click on the new icon (on the top left of the dialog).
10. Fill in Name: `Build`
11. Fill in Gradle Tasks: `build`
12. Fill in Working Directory by clicking on Workspace and selecting FRCBase.
13. Click 'Apply'.

That's all you need to add a build task. You should repeat steps 9-13 for the following build tasks as well (replacing name and tasks with the appropriate name):
- Deploy (deploy)
- Smart Dashboard (smartDashboard)
- Offline Deploy (build deploy --offline)

To get these to show in Eclipse's run dropdown, you either need to have ran the configuration from the set up menu or you need to specify them as a "favorite". Here's the steps to do this:

1. Head to run configurations.
2. Click on the task you want to pin.
3. Go over to the `Common` tab
4. Tick the box in `Display in favorites menu` next to `Run`.

## Updating GradleRIO
To upgrade your version of GradleRIO, you must first upgrade gradle. Near the bottom of your build.gradle, change the wrapper version to the following, and then run `./gradlew wrapper`:
```gradle
task wrapper(type: Wrapper) {
    gradleVersion = '4.4'
}
```

Next, replace the version in the plugin line (only change the GradleRIO line):
```gradle
plugins {
    // ... other plugins ...
    id "jaci.openrio.gradle.GradleRIO" version "2018.01.15"
}
```

## GradleRIO command reference
Here's a collection of some useful GradleRIO commands and tips for development. Reading the full documentation [here](https://github.com/Open-RIO/GradleRIO) is recommended.

- `build` will build your code.
- `deploy` will build and deploy your code.
- `deploy --offline` will build and deploy your code over ethernet.
- `riolog` will display the RoboRIO console output.
- `shuffleboard` will launch Smart Dashboard.
- `clean` will clean your project directory.

You can chain multiple commands in your build configuration if you so desire by separating your build tasks with a space like `deploy shuffleboard` or `deploy riolog`.
