# Overview

**Snippets** provide direct-to-point and practical references for many purposes. **Remarks** and further **reference links** will also be provided. **Tags** are used in brackets, sorted **alphabetically** by title.

See **architecture overview document** for further reference locations.

# Basics

Useful Python commands and basic shortcuts:

1. `Ctrl+Space`: Show auto-complete options
2. `dir`, `type`

# Contents

## (Animation; Scene; Editor) Automatically Update scene every x seconds, not in animation mode

Because we can set `timers` to call a function at certain time interval, we should be able to manipulate scene in this manner as well. Though this is quite non-standard way of **updating scene in real time** - or maybe this is exactly how **"playback animation"** works - by updating whole scene.

```python
# Use bpy.app.timers.register(fun_name, first_interval=seconds) to set a timed routine
(Pending...)
```

## (Addon) Add addon class properties


```python
import bpy

# Blender 2.7
class MyOperator(Operator):
    value = IntProperty() # From bpy.props

# Blender 2.8
class MyOperator(Operator):
    value: IntProperty()
```

## (Mesh; Scene Management) Create a new mesh and add to the scene

```python
mesh = B.meshes.new(name="my mesh")
```

## (Addon; UI) Create a simple Addon

```python
# Blender 2.7
bl_info = {"name": "My Test Add-on", "category": "Object"}
def register():
    print("Hello World")
def unregister():
    print("Goodbye World")
```

```python
# Blender 2.7
# Create an add-on and register a simple operator
bl_info = {
    "name": "Move X Axis",
    "category": "Object",
}

import bpy

class ObjectMoveX(bpy.types.Operator):
    """My Object Moving Script"""      # Use this as a tooltip for menu items and buttons.
    bl_idname = "object.move_x"        # Unique identifier for buttons and menu items to reference.
    bl_label = "Move X by One"         # Display name in the interface.
    bl_options = {'REGISTER', 'UNDO'}  # Enable undo for the operator.

    def execute(self, context):        # execute() is called when running the operator.
        # A script to move objects in the scene
        scene = context.scene
        for obj in scene.objects:
            obj.location.x += 1.0
        return {'FINISHED'}            # Lets Blender know the operator finished successfully.

def register():
    bpy.utils.register_class(ObjectMoveX)


def unregister():
    bpy.utils.unregister_class(ObjectMoveX)


# This allows you to run the script directly from Blender's Text editor
# to test the add-on without having to install it.
if __name__ == "__main__":
    register()
```

```python
# Blender 2.8
bl_info = {
	"name": "My Test Add-on", 
	"category": "Object", 
	"blender": (2, 80, 0)	# This line is important
}

def register():
    print("Hello World")

def unregister():
    print("Goodbye")
```

```yaml
bl_info: a dictionary containing add-on metadata such as the title, version and author to be displayed in the User Preferences add-on list.
register: a function which only runs when enabling the add-on, this means the module can be loaded without activating the add-on.
unregister: a function to unload anything setup by register, this is called when the add-on is disabled.
```

**Installation**: Add-ons are installed through **User Preference**.

**Remark**: Addon is Blender's way to **package codes**. An add on can **subscribe** to some events, and register **operators**, **panels** and **menu items**. An addon's function can be achieved directly through **Python Console** and **Text Editor** in Blender through `bpy` module. Installing add-ons will automatically make a copy from source to blender's `scripts/addons` folder.

**Notice**: 

1. Notice in **Blender 2.8** add-on templates are available in **Text Editor**.
2. (Per reference link below) "Rather than using `bpy.context.scene`, we use the `context.scene` argument passed to `execute()`. In most cases these will be the same. However in some cases, operators will be passed a custom context so script authors should prefer the `context` argument passed to operators."
3. Newly registered operators can be accessed through 

**Reference**: 

* [Blender 2.7 Add-on Tutorial](https://docs.blender.org/manual/en/latest/advanced/scripting/addon_tutorial.html)
* [`bl_info` Dictionary](#)
* [Blender 2.8 Add-on Example](https://wiki.blender.org/wiki/Reference/Release_Notes/2.80/Python_API/Addons) - mentioned `bpy.utils.register_classes_factory` function

## () Startup Script

```python

```

## (Addon) Find addon paths

```python
import addon_utils
print(addon_utils.paths())
```

## (Mesh) Generate Custom A Mesh Using Code

```Python

```

## (Scene) get objects that are selected without using `bpy.context`

```python
selected_objects = [ o for o in bpy.context.scene.objects if o.select ]
```

## (CSV; Data; Mesh Generation) Read a CSV and generate points from CSV data

```python

```

## (Mesh; Animation) Time-Based Transformation Animation

## (Mesh; Scene Management) Transform Objects in the Scene

```python
import bpy

scene = bpy.context.scene
for obj in scene.objects:
    obj.location.x += 1.0
```

## (Procedural Animation) Mesh Deformation, Swing