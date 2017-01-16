# The WillowTree C# Style Guide

Our overarching goals are **conciseness**, **readability** and **simplicity**.

## Table of Contents

- [Nomenclature](#nomenclature)
  + [Namespaces](#namespaces)
  + [Classes & Interfaces](#classes--interfaces)
  + [Methods](#methods)
  + [Fields](#fields)
  + [Parameters](#parameters--parameters)
  + [Delegates](#delegates--delegates)
  + [Events](#events--events)
  + [Misc](#misc)
- [Declarations](#declarations)
  + [Access Level Modifiers](#access-level-modifiers)
  + [Fields & Variables](#fields--variables)
  + [Classes](#classes)
  + [Interfaces](#interfaces)
- [Spacing](#spacing)
  + [Indentation](#indentation)
  + [Line Length](#line-length)
  + [Vertical Spacing](#vertical-spacing)
- [Brace Style](#brace-style)
- [Switch Statements](#switch-statements)
- [Language](#language)
- [Credit](#credits)


## Nomenclature

On the whole, naming should follow C# standards.

### Namespaces

Namespaces are all **PascalCase**, multiple words concatenated together, without hypens ( - ) or underscores ( \_ ). Namespaces should **not** follow reverse domain conventions as is common in Java: 

**BAD**:

```csharp
com.willowtree.project.component
```

**GOOD**:

```csharp
WillowTree.Project.Component
```

### Classes & Interfaces

Written in **PascalCase**. For example `RadialSlider`. 

### Methods

Methods are written in **PascalCase**. For example `DoSomething()`. 

### Fields and Properties

All private fields (including backing fields) are written with a preceding underscore in **camelCase**.  All Properties are written in **PascalCase**.

Public and protected fields should be avoided in favor of public properties.

For example:

```csharp
public class MyClass 
{
    public int PublicField { get; set; }
    int _packagePrivate;
    private int _myBackedProperty;
    public int MyBackedProperty
    {
        get { return _myBackedProperty; }
        set { _myBackedProperty = value; }
    }

    protected int MyProtected { get; set; }
}
```

**BAD:**

```csharp
public class MyClass 
{
    private int myPrivateVariable;
    public int publicField;
}
```

The one exception to this is if you are working with Unity. These standards go against Unity convention, and you should feel free to ignore them in that case.


Static fields are the exception and should be written in **PascalCase**:

```csharp
public static readonly int TheAnswer = 42;
```


### Parameters

Parameters are written in **camelCase**.

**BAD:**

```csharp
void doSomething(Vector3 Location)
```
**GOOD:**

```csharp
void DoSomething(Vector3 location)
```

Single character values are to be avoided except for temporary looping variables.

### Delegates and EventHandlers

Delegates are written in **PascalCase**.

When declaring delegates, DO add the suffix **EventHandler** to names of delegates that are used in events. 

By converntion, .NET event handlers always take 2 parameters: a sender and an EventArgs derived class. You should follow this convention when declaring event handlers.

**BAD:**

```csharp
public delegate void Click()
```
**GOOD:**

```csharp
public delegate void ClickEventHandler(object sender, EventArgs e)
```  

DO add the suffix **Callback** to names of delegates other than those used as event handlers.

**BAD:**

```csharp
public delegate void Render()
```
**GOOD:**

```csharp
public delegate void RenderCallback()
```  

In most cases is is may be better to use ***Action<T>*** or ***Func<T>*** for these over explicity declared callbacks.

### Events

Following Microsoft's naming conventions on events:
* **DO** name events with a verb or a verb phrase.
* **DO** give events names with a concept of before and after, using the present and past tenses. For example, a close event that is raised before a window is closed would be called Closing, and one that is raised after the window is closed would be called Closed.
* **DO NOT** use "Before" or "After" prefixes or postfixes to indicate pre- and post-events. Use present and past tenses as just described.
* **DO** name event argument classes with the "EventArgs" suffix
* **DO NOT** prefix events with **On**. This should be reserved for protected virtual methods used to raise events.

**GOOD:**

```csharp
public event ClosedEventHandler Closed;
```

**BAD:**

```csharp
public event CloseCallback OnClose;
```  


### Misc

In code, acronyms should be treated as words. For example:

**BAD:**

```csharp
XMLHTTPRequest
String URL
findPostByID
```  

**GOOD:**

```csharp
XmlHttpRequest
String url
findPostById
```

## Declarations

### Access Level Modifiers

Access level modifiers should be explicitly defined for classes, methods and member variables.

### Fields & Variables

Prefer single declaration per line.

**BAD:**

```csharp
string username, twitterHandle;
```

**GOOD:**

```csharp
string username;
string twitterHandle;
```

### Classes

Exactly one class per source file, although inner classes are encouraged where scoping appropriate.

Interfaces that have one explicit implementation (service classes for example) *may* be declared in the same file as the classes that implement them.

### Interfaces

All interfaces should be prefaced with the letter **I**. 

**BAD:**

```csharp
RadialSlider
```

**GOOD:**

```csharp
IRadialSlider
```

## Spacing

### Indentation

Indentation should be done using **spaces** — never tabs.  

#### Blocks

Indentation for blocks uses **4 spaces** for optimal readability:

**BAD:**

```csharp
for (int i = 0; i < 10; i++) 
{
  Debug.Log("index=" + i);
}
```

**GOOD:**

```csharp
for (int i = 0; i < 10; i++) 
{
    Debug.Log("index=" + i);
}
```

#### Line Wraps

Indentation for line wraps should use **4 spaces** (not the default 8):

**BAD:**

```csharp
CoolUiWidget widget =
        someIncrediblyLongExpression(that, reallyWouldNotFit, on, aSingle, line);
```

**GOOD:**

```csharp
CoolUiWidget widget =
    someIncrediblyLongExpression(that, reallyWouldNotFit, on, aSingle, line);
```

### Vertical Spacing

There should be exactly one blank line between methods to aid in visual clarity 
and organization. Whitespace within methods should separate functionality, but 
having too many sections in a method often means you should refactor into
several methods.

## Brace Style

All braces get their own line as it is a C# convention:

**BAD:**

```csharp
class MyClass {
    void DoSomething() {
        if (someTest) {
          // ...
        } else {
          // ...
        }
    }
}
```

**GOOD:**

```csharp
class MyClass
{
    void DoSomething()
    {
        if (someTest)
        {
          // ...
        }
        else
        {
          // ...
        }
    }
}
```

Conditional statements are always required to be enclosed with braces,
irrespective of the number of lines required.

**BAD:**

```csharp
if (someTest)
    doSomething();  

if (someTest) doSomethingElse();
```

**GOOD:**

```csharp
if (someTest) 
{
    doSomething();
}  

if (someTest) { doSomethingElse(); }
```

## Switch Statements

Switch-statements come with `default` case by default (heh). When your code is written correctly, it should never reach this part.
Never include the `default` case.

**BAD:**  
  
```csharp
switch (variable) 
{
    case 1:
        break;
    case 2:
        break;
    default:
        break;
}
```

**GOOD:**  
  
```csharp
switch (variable) 
{
    case 1:
        break;
    case 2:
        break;
}
```

## Language

Use US English spelling.

**BAD:**

```csharp
string colour = "red";
```

**GOOD:**

```csharp
string color = "red";
```

## Credits

This style guide was forked from the collaborative effort from the most stylish
raywenderlich.com team members:

- [Darryl Bayliss](https://github.com/DarrylBayliss)
- [Sam Davies](https://github.com/sammyd)
- [Mic Pringle](https://github.com/micpringle)
- [Brian Moakley](https://github.com/VegetarianZombie)
- [Ray Wenderlich](https://github.com/rwenderlich)
- [Eric Van de Kerckhove](https://github.com/BlackDragonBE)

