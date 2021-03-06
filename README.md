#Dock / Snap Example by OpenFin

## Dock & Snap Approach
The intention of this repo is to provide developers a general (yet uniform) approach to docking and snapping windows within their apps while utilizing OpenFin. By design, the approach is generic and not intended to solve specific application use cases. Many applications and application developers have varying opinions as to the behavoir of window docking & snapping. Our thought here is to provide a framework for those app developers to have as a guide, but provide the flexibility and optionality to solve for their own unique use cases. PLEASE BE AWARE THAT THIS IS NOT A PRODUCT AND CONSIDER CLONING THIS PROJECT TO USE IT.   

## Assumptions
* This sample project is a baseline set of features for Snap & Dock
* Edge cases are NOT a functionality driver for this sample
* Docked windows are not resizable

## Current Features
* Window snapping while dragging close to other windows
* Docking snapped windows on release. 
* Windows snap and align both vertically and/or horizontally
* All docked windows in a group display an undock icon
* Clicking the undock icon will seperate the window from the rest of the docked windows.
* Single window can be docked to a group of docked window, but group of docked windows cannot join another group or window.

## Edge Cases Supported
* If docked windows are undocked off monitor, the windows off monitor(s) come back into view



# To See this Demo
* click this [openfin installer download](https://dl.openfin.co/services/download?fileName=snap-and-dock-installer&config=http://openfin.github.io/snap-and-dock/app.json)
* unzip and run the installer
* double click the icon it creates on your desktop

# How to use

## From main window
1. Add DockingManager.js in your project.
2. Creating new instance of DockingManager. like ```var dockingManager = new DockingManager();```
3. Register instances of Openfin Windows (fin.desktop.Window) with DockingManager. ```dockingManager.register(fin.desktop.Window.getCurrent());```
4. If you want a window to not dock to others but only others dock to it you can pass false as the second argument of dockingManager.register
```dockingManager.register(fin.desktop.Window.getCurrent(), false)```


## From Child Window

 1. You can subscribe to docking events (window-docked, window-undocked) to get notified when child window gets docked to another window.
e.g. ```fin.desktop.InterApplicationBus.subscribe("*", "window-docked", onDock);
     fin.desktop.InterApplicationBus.subscribe("*", "window-undocked", onUnDock);```

     As these messages are sent as a broadcast to all windows. you will need to filter these by windowName key which is sent as part of the message.

 2. To undock you will need to send an undock message (undock-winodw) with window name passed as part of the message.
 e.g.
 ``` fin.desktop.InterApplicationBus.publish("undock-window", { windowName: window.name });```

## From External Windows

External windows, such as Java windows, can also register with Docking Manager to have Snap and Dock functionalties.  Please refer to [Java Example](https://github.com/openfin/java-example) as an example.

 And thats all!

 For more details, please have a look at the code in this project.


