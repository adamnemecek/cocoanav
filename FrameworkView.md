FrameworkView is the main display class, displaying frameworks and classes in two modes :

  * Framework : frameworks are displayed arranged in a grid, each holding all its classes
  * ClassTree : frameworks are no longer shows, rather classes are displayed in an inheritance tree, linked to their parent and children — each class is drawn with the background color of its framework

FrameworkView is a CoreAnimation class. In framework view, frameworks get a CALayer and a CATextLayer to display their title. In ClassTree view, classes are visually linked by CALayers. Class names are displayed by CATextLayer.

You can move around the view by dragging the mouse, and zoom with the wheel.

You can select a class by clicking on it, it will be hilighted by a selection layer overlaid on top of the CATextLayer.


FrameworkView stores all its layers in a container layer called frameworksLayer. The perspective transform is set on that layer.

FrameworkView uses a helper layer to convert coordinates from NSView to the CALayer. This is used while dragging and zooming.