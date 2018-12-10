---
title: Increase NURBS Curve Degree
description: Demonstrates how to increase the degree of a NURBS curve.
authors: ['steve_baer']
sdk: ['RhinoCommon']
languages: ['C#', 'Python', 'VB']
platforms: ['Windows', 'Mac']
categories: ['Curves']
origin: http://wiki.mcneel.com/developer/rhinocommonsamples/nurbscurveincreasedegree
order: 1
keywords: ['increasing', 'degree', 'nurbs', 'curve']
layout: code-sample-rhinocommon
---

```cs
partial class Examples
{
  public static Result NurbsCurveIncreaseDegree(RhinoDoc doc)
  {
    ObjRef obj_ref;
    var rc = RhinoGet.GetOneObject(
      "Select curve", false, ObjectType.Curve, out obj_ref);
    if (rc != Result.Success) return rc;
    if (obj_ref == null) return Result.Failure;
    var curve = obj_ref.Curve();
    if (curve == null) return Result.Failure;
    var nurbs_curve = curve.ToNurbsCurve();

    int new_degree = -1;
    rc = RhinoGet.GetInteger(string.Format("New degree <{0}...11>", nurbs_curve.Degree), true, ref new_degree,
      nurbs_curve.Degree, 11);
    if (rc != Result.Success) return rc;

    rc = Result.Failure;
    if (nurbs_curve.IncreaseDegree(new_degree))
      if (doc.Objects.Replace(obj_ref.ObjectId, nurbs_curve))
        rc = Result.Success;

    RhinoApp.WriteLine("Result: {0}", rc.ToString());
    doc.Views.Redraw();
    return rc;
  }
}
```
{: #cs .tab-pane .fade .in .active}


```vbnet
Partial Friend Class Examples
  Public Shared Function NurbsCurveIncreaseDegree(ByVal doc As RhinoDoc) As Result
	Dim obj_ref As ObjRef = Nothing
	Dim rc = RhinoGet.GetOneObject("Select curve", False, ObjectType.Curve, obj_ref)
	If rc IsNot Result.Success Then
		Return rc
	End If
	If obj_ref Is Nothing Then
		Return Result.Failure
	End If
	Dim curve = obj_ref.Curve()
	If curve Is Nothing Then
		Return Result.Failure
	End If
	Dim nurbs_curve = curve.ToNurbsCurve()

	Dim new_degree As Integer = -1
	rc = RhinoGet.GetInteger(String.Format("New degree <{0}...11>", nurbs_curve.Degree), True, new_degree, nurbs_curve.Degree, 11)
	If rc IsNot Result.Success Then
		Return rc
	End If

	rc = Result.Failure
	If nurbs_curve.IncreaseDegree(new_degree) Then
	  If doc.Objects.Replace(obj_ref.ObjectId, nurbs_curve) Then
		rc = Result.Success
	  End If
	End If

	RhinoApp.WriteLine("Result: {0}", rc.ToString())
	doc.Views.Redraw()
	Return rc
  End Function
End Class
```
{: #vb .tab-pane .fade .in}


```python
from Rhino import *
from Rhino.Commands import *
from Rhino.Input import *
from Rhino.DocObjects import *
from scriptcontext import doc

def RunCommand():
    rc, obj_ref = RhinoGet.GetOneObject("Select curve", False, ObjectType.Curve)
    if rc != Result.Success: return rc
    if obj_ref == None: return Result.Failure
    curve = obj_ref.Curve()
    if curve == None: return Result.Failure
    nurbs_curve = curve.ToNurbsCurve()

    new_degree = -1
    rc, new_degree = RhinoGet.GetInteger("New degree <{0}...11>".format(nurbs_curve.Degree), True, new_degree, nurbs_curve.Degree, 11)
    if rc != Result.Success: return rc

    rc = Result.Failure
    if nurbs_curve.IncreaseDegree(new_degree):
        if doc.Objects.Replace(obj_ref.ObjectId, nurbs_curve):
            rc = Result.Success

    print "Result: {0}".format(rc)
    doc.Views.Redraw()
    return rc

if __name__ == "__main__":
    RunCommand()
```
{: #py .tab-pane .fade .in}
