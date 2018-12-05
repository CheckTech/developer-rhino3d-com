---
title: Determine Active Viewport
description: Demonstrates how to determine the active viewport name, even in a layout or a detail view.
authors: ['steve_baer']
author_contacts: ['stevebaer']
sdk: ['RhinoCommon']
languages: ['C#', 'Python', 'VB']
platforms: ['Windows', 'Mac']
categories: ['Viewports and Views']
origin: http://wiki.mcneel.com/developer/rhinocommonsamples/activeviewport
order: 1
keywords: ['determine', 'active', 'viewport']
layout: code-sample-rhinocommon
---

```cs
partial class Examples
{
  public static Rhino.Commands.Result ActiveViewport(Rhino.RhinoDoc doc)
  {
    Rhino.Display.RhinoView view = doc.Views.ActiveView;
    if (view == null)
      return Rhino.Commands.Result.Failure;

    Rhino.Display.RhinoPageView pageview = view as Rhino.Display.RhinoPageView;
    if (pageview != null)
    {
      string layout_name = pageview.PageName;
      if (pageview.PageIsActive)
      {
        Rhino.RhinoApp.WriteLine("The layout {0} is active", layout_name);
      }
      else
      {
        string detail_name = pageview.ActiveViewport.Name;
        Rhino.RhinoApp.WriteLine("The detail {0} on layout {1} is active", detail_name, layout_name);
      }
    }
    else
    {
      string viewport_name = view.MainViewport.Name;
      Rhino.RhinoApp.WriteLine("The viewport {0} is active", viewport_name);
    }
    return Rhino.Commands.Result.Success;
  }
}
```
{: #cs .tab-pane .fade .in .active}


```vbnet
Partial Friend Class Examples
  Public Shared Function ActiveViewport(ByVal doc As Rhino.RhinoDoc) As Rhino.Commands.Result
	Dim view As Rhino.Display.RhinoView = doc.Views.ActiveView
	If view Is Nothing Then
	  Return Rhino.Commands.Result.Failure
	End If

	Dim pageview As Rhino.Display.RhinoPageView = TryCast(view, Rhino.Display.RhinoPageView)
	If pageview IsNot Nothing Then
	  Dim layout_name As String = pageview.PageName
	  If pageview.PageIsActive Then
		Rhino.RhinoApp.WriteLine("The layout {0} is active", layout_name)
	  Else
		Dim detail_name As String = pageview.ActiveViewport.Name
		Rhino.RhinoApp.WriteLine("The detail {0} on layout {1} is active", detail_name, layout_name)
	  End If
	Else
	  Dim viewport_name As String = view.MainViewport.Name
	  Rhino.RhinoApp.WriteLine("The viewport {0} is active", viewport_name)
	End If
	Return Rhino.Commands.Result.Success
  End Function
End Class
```
{: #vb .tab-pane .fade .in}


```python
import Rhino
import scriptcontext

def ActiveViewport():
    view = scriptcontext.doc.Views.ActiveView
    if view is None: return
    if isinstance(view, Rhino.Display.RhinoPageView):
        if view.PageIsActive:
            print "The layout", view.PageName, "is active"
        else:
            detail_name = view.ActiveViewport.Name
            print "The detail", detail_name, "on layout", view.PageName, "is active"
    else:
        print "The viewport", view.MainViewport.Name, "is active"


if __name__ == "__main__":
    ActiveViewport()
```
{: #py .tab-pane .fade .in}
