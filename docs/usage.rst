=====
Usage
=====

DaVinci Resolve API in a project::
----------------------------------
from davinci_resolve_api.Folder import Folder
from davinci_resolve_api.Gallery import Gallery
from davinci_resolve_api.MediaPool import MediaPool
...

README
------
Blackmagic Design DaVinci Resolve README:
C:/ProgramData/Blackmagic Design/DaVinci Resolve/Support/Developer/Scripting/README.txt

Overview
--------
As with Blackmagic Design Fusion scripts, user scripts written in Lua and Python programming languages are supported. By default, scripts can be invoked from the Console window in the Fusion page,
or via command line. This permission can be changed in Resolve Preferences, to be only from Console, or to be invoked from the local network. Please be aware of the security implications when
allowing scripting access from outside of the Resolve application.

Prerequisites
-------------
DaVinci Resolve API scripting requires(for all users):
Python 3.6 64-bit

Basic Resolve API (from Blackmagic Design DaVinci Resolve README:)
-----------------

Resolve
  Fusion()                                        --> Fusion             Comment: Returns the Fusion object. Starting point for Fusion scripts.
  GetMediaStorage()                               --> MediaStorage       Comment: Returns the media storage object to query and act on media locations.
  GetProjectManager()                             --> ProjectManager     Comment: Returns the project manager object for currently open database.
  OpenPage(pageName)                              --> Bool               Comment: Switches to indicated page in DaVinci Resolve. Input can be one of ("media", "cut", "edit", "fusion", "color", "fairlight", "deliver").
  GetCurrentPage()                                --> String             Comment: Returns the page currently displayed in the main window. Returned value can be one of ("media", "cut", "edit", "fusion", "color", "fairlight", "deliver", None).
  GetProductName()                                --> string             Comment: Returns product name.
  GetVersion()                                    --> [version fields]   Comment: Returns list of product version fields in [major, minor, patch, build, suffix] format.
  GetVersionString()                              --> string             Comment: Returns product version in "major.minor.patch[suffix].build" format.
  LoadLayoutPreset(presetName)                    --> Bool               Comment: Loads UI layout from saved preset named 'presetName'.
  UpdateLayoutPreset(presetName)                  --> Bool               Comment: Overwrites preset named 'presetName' with current UI layout.
  ExportLayoutPreset(presetName, presetFilePath)  --> Bool               Comment: Exports preset named 'presetName' to path 'presetFilePath'.
  DeleteLayoutPreset(presetName)                  --> Bool               Comment: Deletes preset named 'presetName'.
  SaveLayoutPreset(presetName)                    --> Bool               Comment: Saves current UI layout as a preset named 'presetName'.
  ImportLayoutPreset(presetFilePath, presetName)  --> Bool               Comment: Imports preset from path 'presetFilePath'. The optional argument 'presetName' specifies how the preset shall be named. If not specified, the preset is named based on the filename.
  Quit()                                          --> None               Comment: Quits the Resolve App.

ProjectManager
  CreateProject(projectName)                      --> Project            Comment: Creates and returns a project if projectName (string) is unique, and None if it is not.
  DeleteProject(projectName)                      --> Bool               Comment: Delete project in the current folder if not currently loaded
  LoadProject(projectName)                        --> Project            Comment: Loads and returns the project with name = projectName (string) if there is a match found, and None if there is no matching Project.
  GetCurrentProject()                             --> Project            Comment: Returns the currently loaded Resolve project.
  SaveProject()                                   --> Bool               Comment: Saves the currently loaded project with its own name. Returns True if successful.
  CloseProject(project)                           --> Bool               Comment: Closes the specified project without saving.
  CreateFolder(folderName)                        --> Bool               Comment: Creates a folder if folderName (string) is unique.
  DeleteFolder(folderName)                        --> Bool               Comment: Deletes the specified folder if it exists. Returns True in case of success.
  GetProjectListInCurrentFolder()                 --> [project names...] Comment: Returns a list of project names in current folder.
  GetFolderListInCurrentFolder()                  --> [folder names...]  Comment: Returns a list of folder names in current folder.
  GotoRootFolder()                                --> Bool               Comment: Opens root folder in database.
  GotoParentFolder()                              --> Bool               Comment: Opens parent folder of current folder in database if current folder has parent.
  GetCurrentFolder()                              --> string             Comment: Returns the current folder name.
  OpenFolder(folderName)                          --> Bool               Comment: Opens folder under given name.
  ImportProject(filePath)                         --> Bool               Comment: Imports a project from the file path provided. Returns True if successful.
  ExportProject(projectName, filePath, withStillsAndLUTs=True) --> Bool  Comment: Exports project to provided file path, including stills and LUTs if withStillsAndLUTs is True (enabled by default). Returns True in case of success.
  RestoreProject(filePath)                        --> Bool               Comment: Restores a project from the file path provided. Returns True if successful.
  GetCurrentDatabase()                            --> {dbInfo}           Comment: Returns a dictionary (with keys 'DbType', 'DbName' and optional 'IpAddress') corresponding to the current database connection
  GetDatabaseList()                               --> [{dbInfo}]         Comment: Returns a list of dictionary items (with keys 'DbType', 'DbName' and optional 'IpAddress') corresponding to all the databases added to Resolve
  SetCurrentDatabase({dbInfo})                    --> Bool               Comment: Switches current database connection to the database specified by the keys below, and closes any open project.
                                                                         Comment: 'DbType': 'Disk' or 'PostgreSQL' (string)
                                                                         Comment: 'DbName': database name (string)
                                                                         Comment: 'IpAddress': IP address of the PostgreSQL server (string, optional key - defaults to '127.0.0.1')

Project
  GetMediaPool()                                  --> MediaPool          Comment: Returns the Media Pool object.
  GetTimelineCount()                              --> int                Comment: Returns the number of timelines currently present in the project.
  GetTimelineByIndex(idx)                         --> Timeline           Comment: Returns timeline at the given index, 1 <= idx <= project.GetTimelineCount()
  GetCurrentTimeline()                            --> Timeline           Comment: Returns the currently loaded timeline.
  SetCurrentTimeline(timeline)                    --> Bool               Comment: Sets given timeline as current timeline for the project. Returns True if successful.
  GetGallery()                                    --> Gallery            Comment: Returns the Gallery object.
  GetName()                                       --> string             Comment: Returns project name.
  SetName(projectName)                            --> Bool               Comment: Sets project name if given projectname (string) is unique.
  GetPresetList()                                 --> [presets...]       Comment: Returns a list of presets and their information.
  SetPreset(presetName)                           --> Bool               Comment: Sets preset by given presetName (string) into project.
  AddRenderJob()                                  --> string             Comment: Adds a render job based on current render settings to the render queue. Returns a unique job id (string) for the new render job.
  DeleteRenderJob(jobId)                          --> Bool               Comment: Deletes render job for input job id (string).
  DeleteAllRenderJobs()                           --> Bool               Comment: Deletes all render jobs in the queue.
  GetRenderJobList()                              --> [render jobs...]   Comment: Returns a list of render jobs and their information.
  GetRenderPresetList()                           --> [presets...]       Comment: Returns a list of render presets and their information.
  StartRendering(jobId1, jobId2, ...)             --> Bool               Comment: Starts rendering jobs indicated by the input job ids.
  StartRendering([jobIds...], isInteractiveMode=False)    --> Bool       Comment: Starts rendering jobs indicated by the input job ids.
                                                                         Comment: The optional "isInteractiveMode", when set, enables error feedback in the UI during rendering.
  StartRendering(isInteractiveMode=False)                 --> Bool       Comment: Starts rendering all queued render jobs. 
                                                                         Comment: The optional "isInteractiveMode", when set, enables error feedback in the UI during rendering.
  StopRendering()                                 --> None               Comment: Stops any current render processes.
  IsRenderingInProgress()                         --> Bool               Comment: Returns True if rendering is in progress.
  LoadRenderPreset(presetName)                    --> Bool               Comment: Sets a preset as current preset for rendering if presetName (string) exists.
  SaveAsNewRenderPreset(presetName)               --> Bool               Comment: Creates new render preset by given name if presetName(string) is unique.
  SetRenderSettings({settings})                   --> Bool               Comment: Sets given settings for rendering. Settings is a dict, with support for the keys:
                                                                         Comment: Refer to "Looking up render settings" section for information for supported settings
  GetRenderJobStatus(jobId)                       --> {status info}      Comment: Returns a dict with job status and completion percentage of the job by given jobId (string).
  GetSetting(settingName)                         --> string             Comment: Returns value of project setting (indicated by settingName, string). Check the section below for more information.
  SetSetting(settingName, settingValue)           --> Bool               Comment: Sets the project setting (indicated by settingName, string) to the value (settingValue, string). Check the section below for more information.
  GetRenderFormats()                              --> {render formats..} Comment: Returns a dict (format -> file extension) of available render formats.
  GetRenderCodecs(renderFormat)                   --> {render codecs...} Comment: Returns a dict (codec description -> codec name) of available codecs for given render format (string).
  GetCurrentRenderFormatAndCodec()                --> {format, codec}    Comment: Returns a dict with currently selected format 'format' and render codec 'codec'.
  SetCurrentRenderFormatAndCodec(format, codec)   --> Bool               Comment: Sets given render format (string) and render codec (string) as options for rendering.
  GetCurrentRenderMode()                          --> int                Comment: Returns the render mode: 0 - Individual clips, 1 - Single clip.
  SetCurrentRenderMode(renderMode)                --> Bool               Comment: Sets the render mode. Specify renderMode = 0 for Individual clips, 1 for Single clip.
  GetRenderResolutions(format, codec)             --> [{Resolution}]     Comment: Returns list of resolutions applicable for the given render format (string) and render codec (string). Returns full list of resolutions if no argument is provided. Each element in the list is a dictionary with 2 keys "Width" and "Height".
  RefreshLUTList()                                --> Bool               Comment: Refreshes LUT List

MediaStorage
  GetMountedVolumeList()                          --> [paths...]         Comment: Returns list of folder paths corresponding to mounted volumes displayed in Resolve’s Media Storage.
  GetSubFolderList(folderPath)                    --> [paths...]         Comment: Returns list of folder paths in the given absolute folder path.
  GetFileList(folderPath)                         --> [paths...]         Comment: Returns list of media and file listings in the given absolute folder path. Note that media listings may be logically consolidated entries.
  RevealInStorage(path)                           --> Bool               Comment: Expands and displays given file/folder path in Resolve’s Media Storage.
  AddItemListToMediaPool(item1, item2, ...)       --> [clips...]         Comment: Adds specified file/folder paths from Media Storage into current Media Pool folder. Input is one or more file/folder paths. Returns a list of the MediaPoolItems created.
  AddItemListToMediaPool([items...])              --> [clips...]         Comment: Adds specified file/folder paths from Media Storage into current Media Pool folder. Input is an array of file/folder paths. Returns a list of the MediaPoolItems created.
  AddClipMattesToMediaPool(MediaPoolItem, [paths], stereoEye) --> Bool   Comment: Adds specified media files as mattes for the specified MediaPoolItem. StereoEye is an optional argument for specifying which eye to add the matte to for stereo clips ("left" or "right"). Returns True if successful.
  AddTimelineMattesToMediaPool([paths])           --> [MediaPoolItems]   Comment: Adds specified media files as timeline mattes in current media pool folder. Returns a list of created MediaPoolItems.

MediaPool
  GetRootFolder()                                 --> Folder             Comment: Returns root Folder of Media Pool
  AddSubFolder(folder, name)                      --> Folder             Comment: Adds new subfolder under specified Folder object with the given name.
  CreateEmptyTimeline(name)                       --> Timeline           Comment: Adds new timeline with given name.
  AppendToTimeline(clip1, clip2, ...)             --> [TimelineItem]     Comment: Appends specified MediaPoolItem objects in the current timeline. Returns the list of appended timelineItems.
  AppendToTimeline([clips])                       --> [TimelineItem]     Comment: Appends specified MediaPoolItem objects in the current timeline. Returns the list of appended timelineItems.
  AppendToTimeline([{clipInfo}, ...])             --> [TimelineItem]     Comment: Appends list of clipInfos specified as dict of "mediaPoolItem", "startFrame" (int), "endFrame" (int), (optional) "mediaType" (int; 1 - Video only, 2 - Audio only). Returns the list of appended timelineItems.
  CreateTimelineFromClips(name, clip1, clip2,...) --> Timeline           Comment: Creates new timeline with specified name, and appends the specified MediaPoolItem objects.
  CreateTimelineFromClips(name, [clips])          --> Timeline           Comment: Creates new timeline with specified name, and appends the specified MediaPoolItem objects.
  CreateTimelineFromClips(name, [{clipInfo}])     --> Timeline           Comment: Creates new timeline with specified name, appending the list of clipInfos specified as a dict of "mediaPoolItem", "startFrame" (int), "endFrame" (int).
  ImportTimelineFromFile(filePath, {importOptions}) --> Timeline         Comment: Creates timeline based on parameters within given file and optional importOptions dict, with support for the keys:
                                                                         Comment: "timelineName": string, specifies the name of the timeline to be created
                                                                         Comment: "importSourceClips": Bool, specifies whether source clips should be imported, True by default
                                                                         Comment: "sourceClipsPath": string, specifies a filesystem path to search for source clips if the media is inaccessible in their original path and if "importSourceClips" is True
                                                                         Comment: "sourceClipsFolders": List of Media Pool folder objects to search for source clips if the media is not present in current folder and if "importSourceClips" is False
                                                                         Comment: "interlaceProcessing": Bool, specifies whether to enable interlace processing on the imported timeline being created. valid only for AAF import
  DeleteTimelines([timeline])                     --> Bool               Comment: Deletes specified timelines in the media pool.
  GetCurrentFolder()                              --> Folder             Comment: Returns currently selected Folder.
  SetCurrentFolder(Folder)                        --> Bool               Comment: Sets current folder by given Folder.
  DeleteClips([clips])                            --> Bool               Comment: Deletes specified clips or timeline mattes in the media pool
  DeleteFolders([subfolders])                     --> Bool               Comment: Deletes specified subfolders in the media pool
  MoveClips([clips], targetFolder)                --> Bool               Comment: Moves specified clips to target folder.
  MoveFolders([folders], targetFolder)            --> Bool               Comment: Moves specified folders to target folder.
  GetClipMatteList(MediaPoolItem)                 --> [paths]            Comment: Get mattes for specified MediaPoolItem, as a list of paths to the matte files.
  GetTimelineMatteList(Folder)                    --> [MediaPoolItems]   Comment: Get mattes in specified Folder, as list of MediaPoolItems.
  DeleteClipMattes(MediaPoolItem, [paths])        --> Bool               Comment: Delete mattes based on their file paths, for specified MediaPoolItem. Returns True on success.
  RelinkClips([MediaPoolItem], folderPath)        --> Bool               Comment: Update the folder location of specified media pool clips with the specified folder path.
  UnlinkClips([MediaPoolItem])                    --> Bool               Comment: Unlink specified media pool clips.
  ImportMedia([items...])                         --> [MediaPoolItems]   Comment: Imports specified file/folder paths into current Media Pool folder. Input is an array of file/folder paths. Returns a list of the MediaPoolItems created.
  ImportMedia([{clipInfo}])                       --> [MediaPoolItems]   Comment: Imports file path(s) into current Media Pool folder as specified in list of clipInfo dict. Returns a list of the MediaPoolItems created.
                                                                         Comment: Each clipInfo gets imported as one MediaPoolItem unless 'Show Individual Frames' is turned on.
                                                                         Comment: Example: ImportMedia([{"FilePath":"file_%03d.dpx", "StartIndex":1, "EndIndex":100}]) would import clip "file_[001-100].dpx".
  ExportMetadata(fileName, [clips])               --> Bool               Comment: Exports metadata of specified clips to 'fileName' in CSV format.
                                                                         Comment: If no clips are specified, all clips from media pool will be used.

Folder
  GetClipList()                                   --> [clips...]         Comment: Returns a list of clips (items) within the folder.
  GetName()                                       --> string             Comment: Returns the media folder name.
  GetSubFolderList()                              --> [folders...]       Comment: Returns a list of subfolders in the folder.

MediaPoolItem
  GetName()                                       --> string             Comment: Returns the clip name.
  GetMetadata(metadataType=None)                  --> string|dict        Comment: Returns the metadata value for the key 'metadataType'.
                                                                         Comment: If no argument is specified, a dict of all set metadata properties is returned.
  SetMetadata(metadataType, metadataValue)        --> Bool               Comment: Sets the given metadata to metadataValue (string). Returns True if successful.
  SetMetadata({metadata})                         --> Bool               Comment: Sets the item metadata with specified 'metadata' dict. Returns True if successful.
  GetMediaId()                                    --> string             Comment: Returns the unique ID for the MediaPoolItem.
  AddMarker(frameId, color, name, note, duration, --> Bool               Comment: Creates a new marker at given frameId position and with given marker information. 'customData' is optional and helps to attach user specific data to the marker.
            customData)
  GetMarkers()                                    --> {markers...}       Comment: Returns a dict (frameId -> {information}) of all markers and dicts with their information.
                                                                         Comment: Example of output format: {96.0: {'color': 'Green', 'duration': 1.0, 'note': '', 'name': 'Marker 1', 'customData': ''}, ...}
                                                                         Comment: In the above example - there is one 'Green' marker at offset 96 (position of the marker)
  GetMarkerByCustomData(customData)               --> {markers...}       Comment: Returns marker {information} for the first matching marker with specified customData.
  UpdateMarkerCustomData(frameId, customData)     --> Bool               Comment: Updates customData (string) for the marker at given frameId position. CustomData is not exposed via UI and is useful for scripting developer to attach any user specific data to markers.
  GetMarkerCustomData(frameId)                    --> string             Comment: Returns customData string for the marker at given frameId position.
  DeleteMarkersByColor(color)                     --> Bool               Comment: Delete all markers of the specified color from the media pool item. "All" as argument deletes all color markers.
  DeleteMarkerAtFrame(frameNum)                   --> Bool               Comment: Delete marker at frame number from the media pool item.
  DeleteMarkerByCustomData(customData)            --> Bool               Comment: Delete first matching marker with specified customData.
  AddFlag(color)                                  --> Bool               Comment: Adds a flag with given color (string).
  GetFlagList()                                   --> [colors...]        Comment: Returns a list of flag colors assigned to the item.
  ClearFlags(color)                               --> Bool               Comment: Clears the flag of the given color if one exists. An "All" argument is supported and clears all flags.
  GetClipColor()                                  --> string             Comment: Returns the item color as a string.
  SetClipColor(colorName)                         --> Bool               Comment: Sets the item color based on the colorName (string).
  ClearClipColor()                                --> Bool               Comment: Clears the item color.
  GetClipProperty(propertyName=None)              --> string|dict        Comment: Returns the property value for the key 'propertyName'. 
                                                                         Comment: If no argument is specified, a dict of all clip properties is returned. Check the section below for more information.
  SetClipProperty(propertyName, propertyValue)    --> Bool               Comment: Sets the given property to propertyValue (string). Check the section below for more information.
  LinkProxyMedia(proxyMediaFilePath)              --> Bool               Comment: Links proxy media located at path specified by arg 'proxyMediaFilePath' with the current clip. 'proxyMediaFilePath' should be absolute clip path.
  UnlinkProxyMedia()                              --> Bool               Comment: Unlinks any proxy media associated with clip.
  ReplaceClip(filePath)                           --> Bool               Comment: Replaces the underlying asset and metadata of MediaPoolItem with the specified absolute clip path.

Timeline
  GetName()                                       --> string             Comment: Returns the timeline name.
  SetName(timelineName)                           --> Bool               Comment: Sets the timeline name if timelineName (string) is unique. Returns True if successful.
  GetStartFrame()                                 --> int                Comment: Returns the frame number at the start of timeline.
  GetEndFrame()                                   --> int                Comment: Returns the frame number at the end of timeline.
  GetTrackCount(trackType)                        --> int                Comment: Returns the number of tracks for the given track type ("audio", "video" or "subtitle").
  GetItemListInTrack(trackType, index)            --> [items...]         Comment: Returns a list of timeline items on that track (based on trackType and index). 1 <= index <= GetTrackCount(trackType).
  AddMarker(frameId, color, name, note, duration, --> Bool               Comment: Creates a new marker at given frameId position and with given marker information. 'customData' is optional and helps to attach user specific data to the marker.
            customData)
  GetMarkers()                                    --> {markers...}       Comment: Returns a dict (frameId -> {information}) of all markers and dicts with their information.
                                                                         Comment: Example: a value of {96.0: {'color': 'Green', 'duration': 1.0, 'note': '', 'name': 'Marker 1', 'customData': ''}, ...} indicates a single green marker at timeline offset 96
  GetMarkerByCustomData(customData)               --> {markers...}       Comment: Returns marker {information} for the first matching marker with specified customData.
  UpdateMarkerCustomData(frameId, customData)     --> Bool               Comment: Updates customData (string) for the marker at given frameId position. CustomData is not exposed via UI and is useful for scripting developer to attach any user specific data to markers.
  GetMarkerCustomData(frameId)                    --> string             Comment: Returns customData string for the marker at given frameId position.
  DeleteMarkersByColor(color)                     --> Bool               Comment: Deletes all timeline markers of the specified color. An "All" argument is supported and deletes all timeline markers.
  DeleteMarkerAtFrame(frameNum)                   --> Bool               Comment: Deletes the timeline marker at the given frame number.
  DeleteMarkerByCustomData(customData)            --> Bool               Comment: Delete first matching marker with specified customData.
  ApplyGradeFromDRX(path, gradeMode, item1, item2, ...)--> Bool          Comment: Loads a still from given file path (string) and applies grade to Timeline Items with gradeMode (int): 0 - "No keyframes", 1 - "Source Timecode aligned", 2 - "Start Frames aligned".
  ApplyGradeFromDRX(path, gradeMode, [items])     --> Bool               Comment: Loads a still from given file path (string) and applies grade to Timeline Items with gradeMode (int): 0 - "No keyframes", 1 - "Source Timecode aligned", 2 - "Start Frames aligned".
  GetCurrentTimecode()                            --> string             Comment: Returns a string timecode representation for the current playhead position, while on Cut, Edit, Color, Fairlight and Deliver pages.
  SetCurrentTimecode(timecode)                    --> Bool               Comment: Sets current playhead position from input timecode for Cut, Edit, Color, Fairlight and Deliver pages.
  GetCurrentVideoItem()                           --> item               Comment: Returns the current video timeline item.
  GetCurrentClipThumbnailImage()                  --> {thumbnailData}    Comment: Returns a dict (keys "width", "height", "format" and "data") with data containing raw thumbnail image data (RGB 8-bit image data encoded in base64 format) for current media in the Color Page.
                                                                         Comment: An example of how to retrieve and interpret thumbnails is provided in 6_get_current_media_thumbnail.py in the Examples folder.
  GetTrackName(trackType, trackIndex)             --> string             Comment: Returns the track name for track indicated by trackType ("audio", "video" or "subtitle") and index. 1 <= trackIndex <= GetTrackCount(trackType).
  SetTrackName(trackType, trackIndex, name)       --> Bool               Comment: Sets the track name (string) for track indicated by trackType ("audio", "video" or "subtitle") and index. 1 <= trackIndex <= GetTrackCount(trackType).
  DuplicateTimeline(timelineName)                 --> timeline           Comment: Duplicates the timeline and returns the created timeline, with the (optional) timelineName, on success.
  CreateCompoundClip([timelineItems], {clipInfo}) --> timelineItem       Comment: Creates a compound clip of input timeline items with an optional clipInfo map: {"startTimecode" : "00:00:00:00", "name" : "Compound Clip 1"}. It returns the created timeline item.
  CreateFusionClip([timelineItems])               --> timelineItem       Comment: Creates a Fusion clip of input timeline items. It returns the created timeline item.
  ImportIntoTimeline(filePath, {importOptions})   --> Bool               Comment: Imports timeline items from an AAF file and optional importOptions dict into the timeline, with support for the keys:
                                                                         Comment: "autoImportSourceClipsIntoMediaPool": Bool, specifies if source clips should be imported into media pool, True by default
                                                                         Comment: "ignoreFileExtensionsWhenMatching": Bool, specifies if file extensions should be ignored when matching, False by default
                                                                         Comment: "linkToSourceCameraFiles": Bool, specifies if link to source camera files should be enabled, False by default
                                                                         Comment: "useSizingInfo": Bool, specifies if sizing information should be used, False by default
                                                                         Comment: "importMultiChannelAudioTracksAsLinkedGroups": Bool, specifies if multi-channel audio tracks should be imported as linked groups, False by default
                                                                         Comment: "insertAdditionalTracks": Bool, specifies if additional tracks should be inserted, True by default
                                                                         Comment: "insertWithOffset": string, specifies insert with offset value in timecode format - defaults to "00:00:00:00", applicable if "insertAdditionalTracks" is False
                                                                         Comment: "sourceClipsPath": string, specifies a filesystem path to search for source clips if the media is inaccessible in their original path and if "ignoreFileExtensionsWhenMatching" is True
                                                                         Comment: "sourceClipsFolders": string, list of Media Pool folder objects to search for source clips if the media is not present in current folder

  Export(fileName, exportType, exportSubtype)     --> Bool               Comment: Exports timeline to 'fileName' as per input exportType & exportSubtype format.
                                                                         Comment: Refer to section "Looking up timeline exports properties" for information on the parameters.
  GetSetting(settingName)                         --> string             Comment: Returns value of timeline setting (indicated by settingName : string). Check the section below for more information.
  SetSetting(settingName, settingValue)           --> Bool               Comment: Sets timeline setting (indicated by settingName : string) to the value (settingValue : string). Check the section below for more information.
  InsertGeneratorIntoTimeline(generatorName)      --> TimelineItem       Comment: Inserts a generator (indicated by generatorName : string) into the timeline.
  InsertFusionGeneratorIntoTimeline(generatorName) --> TimelineItem      Comment: Inserts a Fusion generator (indicated by generatorName : string) into the timeline.
  InsertOFXGeneratorIntoTimeline(generatorName)   --> TimelineItem       Comment: Inserts an OFX generator (indicated by generatorName : string) into the timeline.
  InsertTitleIntoTimeline(titleName)              --> TimelineItem       Comment: Inserts a title (indicated by titleName : string) into the timeline.
  InsertFusionTitleIntoTimeline(titleName)        --> TimelineItem       Comment: Inserts a Fusion title (indicated by titleName : string) into the timeline.
  GrabStill()                                     --> galleryStill       Comment: Grabs still from the current video clip. Returns a GalleryStill object.
  GrabAllStills(stillFrameSource)                 --> [galleryStill]     Comment: Grabs stills from all the clips of the timeline at 'stillFrameSource' (1 - First frame, 2 - Middle frame). Returns the list of GalleryStill objects.

TimelineItem
  GetName()                                       --> string             Comment: Returns the item name.
  GetDuration()                                   --> int                Comment: Returns the item duration.
  GetEnd()                                        --> int                Comment: Returns the end frame position on the timeline.
  GetFusionCompCount()                            --> int                Comment: Returns number of Fusion compositions associated with the timeline item.
  GetFusionCompByIndex(compIndex)                 --> fusionComp         Comment: Returns the Fusion composition object based on given index. 1 <= compIndex <= timelineItem.GetFusionCompCount()
  GetFusionCompNameList()                         --> [names...]         Comment: Returns a list of Fusion composition names associated with the timeline item.
  GetFusionCompByName(compName)                   --> fusionComp         Comment: Returns the Fusion composition object based on given name.
  GetLeftOffset()                                 --> int                Comment: Returns the maximum extension by frame for clip from left side.
  GetRightOffset()                                --> int                Comment: Returns the maximum extension by frame for clip from right side.
  GetStart()                                      --> int                Comment: Returns the start frame position on the timeline.
  SetProperty(propertyKey, propertyValue)         --> Bool               Comment: Sets the value of property "propertyKey" to value "propertyValue"
                                                                         Comment: Refer to "Looking up Timeline item properties" for more information
  GetProperty(propertyKey)                        --> int/[key:value]    Comment: returns the value of the specified key
                                                                         Comment: if no key is specified, the method returns a dictionary(python) or table(lua) for all supported keys
  AddMarker(frameId, color, name, note, duration, --> Bool               Comment: Creates a new marker at given frameId position and with given marker information. 'customData' is optional and helps to attach user specific data to the marker.
            customData)
  GetMarkers()                                    --> {markers...}       Comment: Returns a dict (frameId -> {information}) of all markers and dicts with their information.
                                                                         Comment: Example: a value of {96.0: {'color': 'Green', 'duration': 1.0, 'note': '', 'name': 'Marker 1', 'customData': ''}, ...} indicates a single green marker at clip offset 96
  GetMarkerByCustomData(customData)               --> {markers...}       Comment: Returns marker {information} for the first matching marker with specified customData.
  UpdateMarkerCustomData(frameId, customData)     --> Bool               Comment: Updates customData (string) for the marker at given frameId position. CustomData is not exposed via UI and is useful for scripting developer to attach any user specific data to markers.
  GetMarkerCustomData(frameId)                    --> string             Comment: Returns customData string for the marker at given frameId position.
  DeleteMarkersByColor(color)                     --> Bool               Comment: Delete all markers of the specified color from the timeline item. "All" as argument deletes all color markers.
  DeleteMarkerAtFrame(frameNum)                   --> Bool               Comment: Delete marker at frame number from the timeline item.
  DeleteMarkerByCustomData(customData)            --> Bool               Comment: Delete first matching marker with specified customData.
  AddFlag(color)                                  --> Bool               Comment: Adds a flag with given color (string).
  GetFlagList()                                   --> [colors...]        Comment: Returns a list of flag colors assigned to the item.
  ClearFlags(color)                               --> Bool               Comment: Clear flags of the specified color. An "All" argument is supported to clear all flags. 
  GetClipColor()                                  --> string             Comment: Returns the item color as a string.
  SetClipColor(colorName)                         --> Bool               Comment: Sets the item color based on the colorName (string).
  ClearClipColor()                                --> Bool               Comment: Clears the item color.
  AddFusionComp()                                 --> fusionComp         Comment: Adds a new Fusion composition associated with the timeline item.
  ImportFusionComp(path)                          --> fusionComp         Comment: Imports a Fusion composition from given file path by creating and adding a new composition for the item.
  ExportFusionComp(path, compIndex)               --> Bool               Comment: Exports the Fusion composition based on given index to the path provided.
  DeleteFusionCompByName(compName)                --> Bool               Comment: Deletes the named Fusion composition.
  LoadFusionCompByName(compName)                  --> fusionComp         Comment: Loads the named Fusion composition as the active composition.
  RenameFusionCompByName(oldName, newName)        --> Bool               Comment: Renames the Fusion composition identified by oldName.
  AddVersion(versionName, versionType)            --> Bool               Comment: Adds a new color version for a video clipbased on versionType (0 - local, 1 - remote).
  GetCurrentVersion()                             --> {versionName...}   Comment: Returns the current version of the video clip. The returned value will have the keys versionName and versionType(0 - local, 1 - remote).
  DeleteVersionByName(versionName, versionType)   --> Bool               Comment: Deletes a color version by name and versionType (0 - local, 1 - remote).
  LoadVersionByName(versionName, versionType)     --> Bool               Comment: Loads a named color version as the active version. versionType: 0 - local, 1 - remote.
  RenameVersionByName(oldName, newName, versionType)--> Bool             Comment: Renames the color version identified by oldName and versionType (0 - local, 1 - remote).
  GetVersionNameList(versionType)                 --> [names...]         Comment: Returns a list of all color versions for the given versionType (0 - local, 1 - remote).
  GetMediaPoolItem()                              --> MediaPoolItem      Comment: Returns the media pool item corresponding to the timeline item if one exists.
  GetStereoConvergenceValues()                    --> {keyframes...}     Comment: Returns a dict (offset -> value) of keyframe offsets and respective convergence values.
  GetStereoLeftFloatingWindowParams()             --> {keyframes...}     Comment: For the LEFT eye -> returns a dict (offset -> dict) of keyframe offsets and respective floating window params. Value at particular offset includes the left, right, top and bottom floating window values.
  GetStereoRightFloatingWindowParams()            --> {keyframes...}     Comment: For the RIGHT eye -> returns a dict (offset -> dict) of keyframe offsets and respective floating window params. Value at particular offset includes the left, right, top and bottom floating window values.
  SetLUT(nodeIndex, lutPath)                      --> Bool               Comment: Sets LUT on the node mapping the node index provided, 1 <= nodeIndex <= total number of nodes.
                                                                         Comment: The lutPath can be an absolute path, or a relative path (based off custom LUT paths or the master LUT path).
                                                                         Comment: The operation is successful for valid lut paths that Resolve has already discovered (see Project.RefreshLUTList).
  SetCDL([CDL map])                               --> Bool               Comment: Keys of map are: "NodeIndex", "Slope", "Offset", "Power", "Saturation", where 1 <= NodeIndex <= total number of nodes.
                                                                         Comment: Example python code - SetCDL({"NodeIndex" : "1", "Slope" : "0.5 0.4 0.2", "Offset" : "0.4 0.3 0.2", "Power" : "0.6 0.7 0.8", "Saturation" : "0.65"})
  AddTake(mediaPoolItem, startFrame, endFrame)    --> Bool               Comment: Adds mediaPoolItem as a new take. Initializes a take selector for the timeline item if needed. By default, the full clip extents is added. startFrame (int) and endFrame (int) are optional arguments used to specify the extents.
  GetSelectedTakeIndex()                          --> int                Comment: Returns the index of the currently selected take, or 0 if the clip is not a take selector.
  GetTakesCount()                                 --> int                Comment: Returns the number of takes in take selector, or 0 if the clip is not a take selector.
  GetTakeByIndex(idx)                             --> {takeInfo...}      Comment: Returns a dict (keys "startFrame", "endFrame" and "mediaPoolItem") with take info for specified index.
  DeleteTakeByIndex(idx)                          --> Bool               Comment: Deletes a take by index, 1 <= idx <= number of takes.
  SelectTakeByIndex(idx)                          --> Bool               Comment: Selects a take by index, 1 <= idx <= number of takes.
  FinalizeTake()                                  --> Bool               Comment: Finalizes take selection.
  CopyGrades([tgtTimelineItems])                  --> Bool               Comment: Copies the current grade to all the items in tgtTimelineItems list. Returns True on success and False if any error occured.

Gallery
  GetAlbumName(galleryStillAlbum)                 --> string             Comment: Returns the name of the GalleryStillAlbum object 'galleryStillAlbum'.
  SetAlbumName(galleryStillAlbum, albumName)      --> Bool               Comment: Sets the name of the GalleryStillAlbum object 'galleryStillAlbum' to 'albumName'.
  GetCurrentStillAlbum()                          --> galleryStillAlbum  Comment: Returns current album as a GalleryStillAlbum object.
  SetCurrentStillAlbum(galleryStillAlbum)         --> Bool               Comment: Sets current album to GalleryStillAlbum object 'galleryStillAlbum'.
  GetGalleryStillAlbums()                         --> [galleryStillAlbum] Comment: Returns the gallery albums as a list of GalleryStillAlbum objects.

GalleryStillAlbum
  GetStills()                                     --> [galleryStill]     Comment: Returns the list of GalleryStill objects in the album.
  GetLabel(galleryStill)                          --> string             Comment: Returns the label of the galleryStill.
  SetLabel(galleryStill, label)                   --> Bool               Comment: Sets the new 'label' to GalleryStill object 'galleryStill'.
  ExportStills([galleryStill], folderPath, filePrefix, format) --> Bool  Comment: Exports list of GalleryStill objects '[galleryStill]' to directory 'folderPath', with filename prefix 'filePrefix', using file format 'format' (supported formats: dpx, cin, tif, jpg, png, ppm, bmp, xpm).
  DeleteStills([galleryStill])                    --> Bool               Comment: Deletes specified list of GalleryStill objects '[galleryStill]'.

GalleryStill                                                             Comment: This class does not provide any API functions but the object type is used by functions in other classes.
