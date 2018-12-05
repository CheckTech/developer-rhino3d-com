---
title: Orthogonal Mode
description: Demonstrates how to enable or disable orthogonal mode and its effects.
authors: ['steve_baer']
author_contacts: ['stevebaer']
sdk: ['RhinoCommon']
languages: ['C#', 'Python', 'VB']
platforms: ['Windows', 'Mac']
categories: ['Other']
origin: http://wiki.mcneel.com/developer/rhinocommonsamples/ortho
order: 1
keywords: ['enabling', 'orthogonal', 'mode']
layout: code-sample-rhinocommon
---

```cs
partial class Examples
{
  public static Result Ortho(RhinoDoc doc)
  {
    var gp = new GetPoint();
    gp.SetCommandPrompt("Start of line");
    gp.Get();
    if (gp.CommandResult() != Result.Success)
      return gp.CommandResult();
    var start_point = gp.Point();

    var original_ortho = ModelAidSettings.Ortho;
    if (!original_ortho)
      ModelAidSettings.Ortho = true;

    gp.SetCommandPrompt("End of line");
    gp.SetBasePoint(start_point, false);
    gp.DrawLineFromPoint(start_point, true);
    gp.Get();
    if (gp.CommandResult() != Result.Success)
      return gp.CommandResult();
    var end_point = gp.Point();

    if (ModelAidSettings.Ortho != original_ortho)
      ModelAidSettings.Ortho = original_ortho;

    doc.Objects.AddLine(start_point, end_point);
    doc.Views.Redraw();
    return Result.Success;
  }
}
```
{: #cs .tab-pane .fade .in .active}


```vbnet
Partial Friend Class Examples
  Public Shared Function Ortho(ByVal doc As RhinoDoc) As Result
	Dim gp = New GetPoint()
	gp.SetCommandPrompt("Start of line")
	gp.Get()
	If gp.CommandResult() <> Result.Success Then
	  Return gp.CommandResult()
	End If
	Dim start_point = gp.Point()

	Dim original_ortho = ModelAidSettings.Ortho
	If Not original_ortho Then
	  ModelAidSettings.Ortho = True
	End If

	gp.SetCommandPrompt("End of line")
	gp.SetBasePoint(start_point, False)
	gp.DrawLineFromPoint(start_point, True)
	gp.Get()
	If gp.CommandResult() <> Result.Success Then
	  Return gp.CommandResult()
	End If
	Dim end_point = gp.Point()

	If ModelAidSettings.Ortho IsNot original_ortho Then
	  ModelAidSettings.Ortho = original_ortho
	End If

	doc.Objects.AddLine(start_point, end_point)
	doc.Views.Redraw()
	Return Result.Success
  End Function
End Class
```
{: #vb .tab-pane .fade .in}


```python
from Rhino import *
from Rhino.ApplicationSettings import *
from Rhino.Commands import *
from Rhino.Input.Custom import *
from scriptcontext import doc

def RunCommand():
  gp = GetPoint()
  gp.SetCommandPrompt("Start of line")
  gp.Get()
  if gp.CommandResult() != Result.Success:
    return gp.CommandResult()
  start_point = gp.Point()

  original_ortho = ModelAidSettings.Ortho
  if not original_ortho:
    ModelAidSettings.Ortho = True

  gp.SetCommandPrompt("End of line")
  gp.SetBasePoint(start_point, False)
  gp.DrawLineFromPoint(start_point, True)
  gp.Get()
  if gp.CommandResult() != Result.Success:
    return gp.CommandResult()
  end_point = gp.Point()

  if ModelAidSettings.Ortho != original_ortho:
    ModelAidSettings.Ortho = original_ortho

  doc.Objects.AddLine(start_point, end_point)
  doc.Views.Redraw()
  return Result.Success

if __name__ == "__main__":
  RunCommand()
```
{: #py .tab-pane .fade .in}
