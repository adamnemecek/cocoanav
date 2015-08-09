CocoaNav parses OSX frameworks and makes them searchable in a nice Core Animation View.

CocoaNav is mostly written in RubyCocoa, with two ObjectiveC classes : [CNItem](CNItem.md) and FrameworkViewBackground. It's a document based app.

[Download CocoaNav](http://inexdo.com/CocoaNav)


## Internals ##

### Model and controllers ###
  * ApplicationController manages data : handles FrameworkParsing, preferences, computing the ClassTree, WalkingTheTree, and [FrameworkColor](FrameworkColor.md)s
  * [CNItem](CNItem.md) is the all purpose data class : it stores parsed class names, methods, protocols and categories
  * CNDocument backs document windows : specifies DocumentType and UserFrameworks
  * FrameworkColor : CoreData class for managing text and background colors of frameworks

### Windows ###
  * CNWindow is the main window : handles coordination between the 3 views : FrameworkView, CrumbView, ItemTableView
  * CNAboutWindow : the about window showing a WebView, backed by a Core Animation Quartz Composition
  * CNPreferencesWindow : handles [FrameworkColor](FrameworkColor.md)s editing

### Views ###
Views ShareSelection.
  * FrameworkViewBackground : draws a radial gradient as a background. This class exists because I couldn't figure out how to draw the gradient with RubyCocoa
  * FrameworkView : the meat of what you'll see. For each Objective C class, creates a matching layer. Two view modes : framework (classes inside their frameworks) or ClassTree (classes linked to their parents)
  * CrumbView : for each class, draws inheritance crumb. For NSButton, draws NSObject > NSResponder > NSControl > NSButton.
  * ItemTableView : displays every framework/class/method/protocol/category loaded and search them


# TODO #
  * better parsing, to handle C methods and structs. Maybe via Pygments. (Then we'll be able to index stuff like CATransform3DMakeScale)
  * when parsing user frameworks,  parse .m files
  * BACK / FORWARD ! maintain a history list, a la Safari
  * it's taking too long on load -> move CNItem to CoreData
  * better refresh on color change
  * (?) UserFrameworks : load all files and make them visually searchable - just like in FrameworkView, to see each instance of a search term
  * UserFrameworks : compute function depth usage and order. Trace usage of one function trough the code, see how deep it's called (call stack), where it's called, by whom
  * parameter use : for each method or function, index its parameters -> see what's being called by whom
  * stuff like Demeter's Law : trail an object to see how deeply it's used
  * real bindings between views : right now it sucks.
  * save document window positions AND contents. via Core Data ? On relaunch, you get exactly what you quit from.
  * framework stats : classes count, method count, …
  * allow user framework removal
  * search within help webview