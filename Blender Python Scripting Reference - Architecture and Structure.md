# Scripting Architecture Overview

The purpose of this doucment is to provide a **high level strucuture presentation** of **Blender Python API** so that we can get a general idea of how API can be integrated in the **modeling process** of Blender and make better use of [blender API Documentation](http://www.blender.org/api/blender_python_api_2_74_5/). 

Further elaboration on this document will focus on **scripted animation** and **tool development for visualization purpose**. **Add-on** and other misc stuff are not of concern to us.

Notice as per Blender 2.8 some of the stuff might be deprecated, *we need ways to maintain this document and keep it up-to-date*.

## Basics and How-Tos

First we mention the very very basic stuff concerning how we can **use Python API**:

1. How to *run Python scripts in Blender*:
    * Use Python Console space type/editor, this supports auto-completion, which is not a good thing to a beginner actually because the prohibits remembers attribute names
    * Use Text Editor space type/editor, use this it will only print errors in Terminal, will not print anything e.g. using list() inside blender python console
2. Data Creation: Notice we cannot create new instances outside the main Blender database using class types directly, must use collections' methods, and we can create variables to hold the references to the objects.
3. How to debug?
    * For simple **print outputs**, we can toggle `Window - Toggle System Console`
4. How is Python Integrated Inside Blender?  
	* Refer to this: https://docs.python.org/3.1/extending/embedding.html

## System Components

**Data Blocks**

1. **Global**: `bpy.types` (Mesh), `bpy.context`
2. **Access by `bpy.data`**, all from current **loaded scene**: `bpy.data.objects`, `bpy.data.scenes`, `bpy.data.materials`, `bpy.data.groups`, `bpy.data.meshes`
3. **Access by `bpy.context`**, used to get active data on the user's selection: `bpy.context.object`, `bpy.context.selected_objects`, `bpy.context.visible_bones`
4. **Generic Accessors and Methods**: `list()`, `[index]` or `["id"]`, `<data_block>.new("id")` or `<data_block>.new(name="id")`, `<data_block>.remove(object_var)`, Get property: `bpy.data.scenes["Scene"].get("test_prop", "fallback value")`, Get property: `object["ObjectProperty"]`

**Data Model**

1. Blend File:
1. **Scenes:**
    * **Members:** `render`, `objects`, `active`
1. **Objects:**
    * **Members:** `name`, `data`
1. Materials
1. **Object.Data:**
    * **Members:** `vertices`
1. **Vertex:**
    * **Members:** `co`

**Uncategorized members:**

1. <scene>.render.resolution_percentage

## Object Model

**Data Types**

1. Internal Blender: `bpy.types.bpy_struct`
2. Native Python: `int`/`float`/`boolean`/`string`/`dictionary`
3. Mathutils: ...
4. ID Types: `bpy.types.bpy_struct` - `bpy.types.ID` - `bpy.types.Object`

# Scene Structure

To script with Python in Blender is to **manipulate objects** within the **scene(s)**, or the Blender file.

The scene most contains containers of following data types: **objects**, **meshes**, **materials**, **textures**, **scenes**, **screens**, **sounds**, **scripts**, *etc.*. All those data are ultimately defined inside `bpy.data`.

Objects in the scene (collections) are **linked/unlinked** together.

## Basic Concepts

Below concepts are mostly relevant to (current) **context**:

1. Object: At any instance, only one object is active and there can be more than one selected object.
2. Context: All objects exist in a context and there can be various modes under which they are operated upon.
3. Mode: The editing mode as in (active) 3D view
4. Blend-file: All objects are data in the blend-file.
5. Operators: operators are functions that create and modify scene objects.
6. Active_object: when multiple objects are selected only the last selected one is the active object.

# Modules

Blender Python API development is broadly divided into below modules for specific tasks:

* **Application Modules**: General Blender Environment, which are datas
* **Standalone Modules**: Helper Libraries Facilitating Creation, math and rendering facilities
* **GameEngine Modules**: Game Engine Specific, logic and game rendering

## Application Modlues:

1. `bpy.data` - Everything in currently loaded `.blend` file: 
    * "`bpy.data` is an instance of the `bpy.types.BlendData` class" as stated [here](http://www.blender.org/api/blender_python_api_2_74_5/info_api_reference.html#simple-data-access).
    * `bpy.context` – Access `bpy.data` according to current **context** (i.e. current **selection of objects** and current **active viewport**), which effectively limits data accessing according to context, and this is **Read Only**
    * `bpy.context.object` is the current active object

## Application Oriented References:
	
1. Mesh Generation: Application Modules
2. User Interface (Panels, Menus) Creation: Application Modules
3. Addons: Application Modules
4. Functions and Scene Data Manipulation, Including Translating Objects and Search: Application Modules

# Other References:

For definition of terminology (for **Blender editor** and environment in general), see **Terminology Reference.xlsx** document.

* General introduction
* Documention of Modules API
* ~/.blender/scripts/startup/bl_ui for the user interface
* ~/.blender/scripts/startup/bl_op for operators
* Help ‣ Operator Cheat Sheet

# Official API Documentation Pointers

1. [Python Examples](https://docs.blender.org/manual/en/latest/editors/python_console.html)
2. [Blender Scene and Object API changes from 2.7x to 2.8](https://wiki.blender.org/wiki/Reference/Release_Notes/2.80/Python_API/Scene_and_Object_API)