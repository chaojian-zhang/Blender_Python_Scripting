People say problems are educative. I am a believer of that.

# Contents

## (bpy.context) "'Context' object has no attribute 'object'"

1. Happens only when run inside Text Editor - works fine in Console

```python
import bpy

def move():
    bpy.context.object.location += 1
    return 1
    
bpy.app.timers.register(move)
```

Cause: Actually inside **Text Editor** we do have access to `bpy.context` and many of its variables, but if the function is registered with **timer** then its `bpy.context` object only have limited items (including `collection` and `scene` but not other variables)

Reference: 

1. [The solution in this link doesn't work](https://blender.stackexchange.com/questions/1922/blender-as-python-module-context-object-has-no-attribute-object)
2. [An illustration of variations of `context` property](https://blender.stackexchange.com/questions/36281/bpy-context-selected-objects-context-object-has-no-attribute-selected-objects?rq=1)
	* Basically "`bpy.context` is usually with **operators** that work in the **3dview** but fail when trying to run them from the python console or when running a script in the text editor."