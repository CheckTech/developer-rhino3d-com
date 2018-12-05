---
title: Loft Surfaces
description: Demonstrates how to create a lofted surface from a set of user-specified curves.
authors: ['steve_baer']
sdk: ['RhinoCommon']
languages: ['C#', 'Python', 'VB']
platforms: ['Windows', 'Mac']
categories: ['Other']
origin: http://wiki.mcneel.com/developer/rhinocommonsamples/loft
order: 1
keywords: ['loft', 'surfaces']
layout: code-sample-rhinocommon
---

```cs
partial class Examples
{
  public static Result Loft(RhinoDoc doc)
  {
    // select curves to loft
    var gs = new GetObject();
    gs.SetCommandPrompt("select curves to loft");
    gs.GeometryFilter = ObjectType.Curve;
    gs.DisablePreSelect();
    gs.SubObjectSelect = false;
    gs.GetMultiple(2, 0);
    if (gs.CommandResult() != Result.Success)
      return gs.CommandResult();

    var curves = gs.Objects().Select(obj => obj.Curve()).ToList();

    var breps = Brep.CreateFromLoft(curves, Point3d.Unset, Point3d.Unset, LoftType.Tight, false);
    foreach (var brep in breps)
      doc.Objects.AddBrep(brep);

    doc.Views.Redraw();
    return Result.Success;
  }
}
```
{: #cs .tab-pane .fade .in .active}


```vbnet
Partial Friend Class Examples
  Public Shared Function Loft(ByVal doc As RhinoDoc) As Result
	' select curves to loft
	Dim gs = New GetObject()
	gs.SetCommandPrompt("select curves to loft")
	gs.GeometryFilter = ObjectType.Curve
	gs.DisablePreSelect()
	gs.SubObjectSelect = False
	gs.GetMultiple(2, 0)
	If gs.CommandResult() <> Result.Success Then
	  Return gs.CommandResult()
	End If

	Dim curves = gs.Objects().Select(Function(obj) obj.Curve()).ToList()

	Dim breps = Brep.CreateFromLoft(curves, Point3d.Unset, Point3d.Unset, LoftType.Tight, False)
	For Each brep In breps
	  doc.Objects.AddBrep(brep)
	Next brep

	doc.Views.Redraw()
	Return Result.Success
  End Function
End Class
```
{: #vb .tab-pane .fade .in}


```python
import rhinoscriptsyntax as rs

def RunCommand():
  crvids = rs.GetObjects(message="select curves to loft", filter=rs.filter.curve, minimum_count=2)
  if not crvids: return

  rs.AddLoftSrf(object_ids=crvids, loft_type = 3) #3 = tight

if __name__ == "__main__":
  RunCommand()
```
{: #py .tab-pane .fade .in}
