---
summary: Use File Viewer Plugin to let users of your mobile app to view remote or app resource files.
tags: runtime-mobile; support-application_development; support-Mobile_Apps;
---

# File Viewer Plugin

Use File Viewer Plugin to create logic that lets users to open remote or app resource files. In Android users select an app to open the file. iOS provides a native preview for supported file types.

File Viewer Plugin can open:

* **File from the app resources**. The plugin can access the **resources** path to load the file that's part of the app static content. See [Working with app resources](#working-with-app-resources)
* **Remote file**. The plugin downloads the file to the app sandbox and then opens the file.

![File Viewer Plugin](images/file-viewer-preview.png?width=300)

## Installing and referencing

To use the plugin, do the following:

1. [Install File Plugin from Forge](https://www.outsystems.com/forge/component-overview/1606/) to your environment. You can also install the demo app to see sample logic for common use cases.

2. In Service Studio, open **Manage Dependencies** (**Ctrl+Q**). 
   
3. Search for **FileViewerPlugin** and select the actions from the plugin.

4. Click **Apply** to add the plugin actions to the app. 

After you reference the File Plugin, you can use the actions in **Logic** > **Client Actions** > **FileViewerPlugin**.

## Viewing files in Android and iOS

To let users view files in the mobile apps, create logic with the action **OpenDocument**. You need to supply a path to a local file in the **FilePath** property or to a remote file in the **URL** property.

If you want to open a file from the app resources see [Working with app resources](#working-with-app-resources).

For an example of how to use the plugin check the demo app or refer to [the example in this document](#example-of-using-file-viewer-plugin).

<div class="info" markdown="1">

For opening media files in the iOS apps, use the action **PreviewMediaContent** from **FileViewerPlugin** > **iOSOnly**. This action lets apps handle the media files better by opening them in a media player.

</div>

## Working with app resources

Here is how to add a file as a resource and open the file with the plugin.

1. In Service Studio, go to the **Data** tab.

2. Right-click the **Resources** folder and select **Import resources**. A file dialog opens, where you can select the file you want to add as a resource.

3. Select the file you added under **Resources**, and:

    * Enter `resources` in the **Target Directory** property. Note that this value must be `resources` and you can't change it.
    * Select **Deploy to Target Directory** in the **Deploy Action** list.

    ![Resources properties for File Viewer](images/resources-file-viewer-ss.png?width=300)

4. In the **OpenDocument** action enter `"resources\<file name>"` in the **FilePath** property. For example, if you add **sample.pdf** to **Resources**, the value of  **FilePath** is `"resources\sample.pdf"`.


<div class="info" markdown="1">

The plugin can access only resources you deploy in the **resources** path. This is a security limitation by design. Limiting access of the plugin prevents accidental access to the resources of the app.

</div>

## Example of using File Viewer Plugin

Here is an example of how to use File Viewer Plugin.

![Open file logic](images/logic-file-viewer-ss.png?width=550)

A good practice is to check if the plugin is available to the app, and report an error if it's not. You can check the plugin availability by using the **CheckPlugin** action and checking the value of the **CheckPlugin.IsAvailable** boolean (1).

When you confirm the plugin is available, use the **OpenDocument** (2) action to ask the operating system to view the file. The action accepts either a **URL** for remote files or **FilePath** for a [file from the app resources](#working-with-app-resources) (3). 

## Reference

More information about parts of the plugin.

### Actions

Here is the reference of the actions you can use from the File Plugin. File Plugin uses a Cordova plugin, and for more information check out [File-Viewer-Plugin](https://github.com/OutSystemsExperts/File-Viewer-Plugin).

| Action                  | Description                                                                          |
| ----------------------- | ------------------------------------------------------------------------------------ |
| **CheckPlugin**         | Checks if the plugin is available in the app.                                        |
| **OpenDocument**        | Opens a remote file or a [file from the app resources](#working-with-app-resources). |
| **PreviewMediaContent** | iOS only. Action to preview media content.                                           |