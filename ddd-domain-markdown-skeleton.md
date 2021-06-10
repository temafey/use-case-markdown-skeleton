# Title

## Table of Contents
+ [Summary](#summary)
+ [Description](#description)
+ [UI/UX](#ui-ux)
+ [Use cases](#use-cases)
+ [Entity object](#entity-object)

## Summary <a name = "summary"></a>
General explanation of a software feature written from the perspective of the end user. 
Its purpose is to articulate how a software feature will provide value to the customer.

## Description <a name = "description"></a>
Formally written declaration of the domain and its idea and context to explain the goals and objectives to be reached, the business need and problem to be addressed, potentials pitfalls and challenges, approaches and execution methods, resource estimates, people and organizations involved, and other relevant information that explains the need for project startup and aims to describe the amount of work planned for implementation.

### UI/UX <a name = "ui-ux"></a>

Basic principles of design and structure, forms, buttons, screens, pages, icons, drawings, visual elements and all things.

Use Case: Name of use case <a name = "use-cases"></a>
=================================
**Actors**: Actor

**Scope**: Software system

**Purpose**: Intention of the use case.

**Type**: Primary (Secondary, Optional)

**Overview**: A brief description of what happens in this use case.

Typical course of events:
----------------------

| Actor Action | System Response |
|:--------------|:----------------|
| 1. This use case begins when Actor wants to initiate an event.| |
| 2. The Actor does something... | 3. The system determines something or responds... |
|4. ||
|5. | 6. |


## Entity object <a name = "entity-object"></a>

For single-item entities the following options are supported, see the section on multi-item entities for the options available for those.

### name (optional)
This allows overriding the display name of the entity, otherwise the friendly name is used

### icon (optional)
Allows overriding the icon of the entity

### content_template (optional)
This allows the display format for that entity to be customised. The format is {{*propertyname*}}. The available properties are:
* **display_name** The entity name (friendly name if not overridden with the name option)
* **state** The state display name (based on device class of entity)

### include_history (optional, defaults to false)
This allows the history of an entity to be displayed, rather than just its current state (states of "unknown" are automatically filtered out).
This currently uses the history for the last day.

### max_history (optional)
The maximum history of the entity to display, this defaults to 3
In addition any attribute of the entity can be used (do not prefix with *attributes.*).

### remove_repeats (optional, defaults to true)
This controls whether to remove repeated states from the history (e.g. the current state is the same as the previous state).
Since "unknown" states are filtered out, this will avoid an entity appearing twice because it changed from "on" to "unknown" and back again following a restart.
This can be disabled by setting this to false.

### state_map (optional)
This allows custom mappings of states to display names, to override the device_class based mappings. In the example below this is used to map the "not_home" state to "Unknown Destination" instead of the default "Away".

### exclude_states (optional)
A list of states to exclude. By default this is just "unknown". For example:
entities:
- entity: sensor.front_door
name: Front Door
exclude_states:
- "off"
- "unknown"

### format (optional, defaults to "relative")
How the timestamp should be formatted.
Valid values are: relative, total, date, time and datetime.

### more_info_on_tap (optional)
This is the same as the option of the same name at the top level. This allows for this setting to be overridden at the entity level.

Example:

    type: 'custom:home-feed-card'
    title: Home Feed
    show_empty: false
    id_filter: ^home_feed_.*
    entities:
      - entity: device_tracker.my_phone
        name: Me
        content_template: '{{display_name}} arrived at {{state}} ({{latitude}},{{longitude}})'
        include_history: true
        max_history: 5
        remove_repeats: false
        state_map:
          not_home: Unknown Destination
