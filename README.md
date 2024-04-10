[![GitHub release (latest by date including pre-releases)](https://img.shields.io/github/v/release/nfa-vfxim/tk-multi-publish2?include_prereleases)](https://github.com/nfa-vfxim/tk-multi-publish2) 
[![GitHub issues](https://img.shields.io/github/issues/nfa-vfxim/tk-multi-publish2)](https://github.com/nfa-vfxim/tk-multi-publish2/issues) 


# Publish <img src="icon_256.png" alt="Icon" height="24"/>

Provides UI and functionality to publish files to ShotGrid.

## Requirements

| ShotGrid version | Core version | Engine version |
|------------------|--------------|----------------|
| -                | v0.19.4      | -              |

**Frameworks:**

| Name                      | Version | Minimum version |
|---------------------------|---------|-----------------|
| tk-framework-shotgunutils | v5.x.x  |                 |
| tk-framework-qtwidgets    | v2.x.x  | v2.7.0          |



## Configuration

### Strings

| Name                  | Description                                                                                                                                                                                                               | Default value |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
| `display_name`        | Specify the name that should be used in menus and the main publish dialog                                                                                                                                                 | Publish       |
| `display_action_name` | Shorter version of display_name setting, used as button name.                                                                                                                                                             | Publish       |
| `help_url`            | The url to open when the 'help' button is clicked in the publisher. The url should typically lead to a page that outlines the studio's publishing workflow. If no url is provided, the help button will not be displayed. |               |


### Hooks

| Name          | Description                                                                                                                                                                                                                                                                                                                          | Default value         |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------|
| `collector`   | Logic for extracting items from the scene and from dropped files.                                                                                                                                                                                                                                                                    | {self}/collector.py   |
| `post_phase`  | A hook that defines logic to be executed after each phase of publish execution including validation, publish, and finalization. This allows for very specific curation and customization of the publish tree during a publish session. Serializing the publish tree to disk after validation, for example is possible via this hook. | {self}/post_phase.py  |
| `path_info`   | This hook contains methods that are used during publishing to infer information from file paths. This includes version and frame number identification, publish display name, image sequence paths, etc.                                                                                                                             | {self}/path_info.py   |
| `pre_publish` | This hook defines logic to be executed before showing the publish dialog. There may be conditions that need to be checked before allowing the user to proceed to publishing.                                                                                                                                                         | {self}/pre_publish.py |


### Dictionaries

| Name                 | Description                                | Default value |
|----------------------|--------------------------------------------|---------------|
| `collector_settings` | Collector-specific configuration settings. | {}            |


### Booleans

| Name                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Default value |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
| `task_required`       | If true validates that a task is selected for every item and disables/enables the validate and publish buttons and finally change the color for the task label.                                                                                                                                                                                                                                                                                                        | False         |
| `validate_on_publish` | If true (default), clicking the Publish button will execute the validation logic before publishing. If false, validation will be skipped. If false, and no validation has been manually triggered, a popup, confirmation dialog will be displayed before proceeding with the publish logic. NOTE: This is an advanced option. Setting this to 'false' will most likely break the shipped toolkit integrations which assume validation is always run before publishing. | True          |
| `enable_manual_load`  | If true (default, normal operation), the user can interact with the main dialog to drop files or folders. The user can also use the browse buttons to select files or folders. When false, the feature basically disable the user ability to add anything to the project.                                                                                                                                                                                              | True          |
| `modal`               | If true the app dialog will be opened in modal window mode, else if false (default) the dialog will be opened in non-modal window mode.                                                                                                                                                                                                                                                                                                                                | False         |


### Lists

| Name              | Description              | Default value                                                                                                                                                          |
|-------------------|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `publish_plugins` | List of publish plugins. | [{'name': 'Publish to ShotGrid', 'hook': '{self}/publish_file.py', 'settings': {}}, {'name': 'Upload for review', 'hook': '{self}/upload_version.py', 'settings': {}}] |


