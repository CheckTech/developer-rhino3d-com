---
title: Object Color
description: Demonstrates how to set the color of user-specified objects.
authors: ['steve_baer']
author_contacts: ['stevebaer']
sdk: ['RhinoCommon']
languages: ['C#', 'VB']
platforms: ['Windows', 'Mac']
categories: ['Adding Objects']
origin: unset
order: 1
keywords: ['object', 'color']
layout: code-sample-rhinocommon
---

```cs
partial class Examples
{
  public static Rhino.Commands.Result ObjectColor(Rhino.RhinoDoc doc)
  {
    Rhino.DocObjects.ObjRef[] objRefs;
    Rhino.Commands.Result cmdResult = Rhino.Input.RhinoGet.GetMultipleObjects("Select objects to change color", false, Rhino.DocObjects.ObjectType.AnyObject, out objRefs);
    if (cmdResult != Rhino.Commands.Result.Success)
      return cmdResult;

    System.Drawing.Color color = System.Drawing.Color.Black;
    bool rc = Rhino.UI.Dialogs.ShowColorDialog(ref color);
    if (!rc)
      return Rhino.Commands.Result.Cancel;

    for (int i = 0; i < objRefs.Length; i++)
    {
      Rhino.DocObjects.RhinoObject obj = objRefs[i].Object();
      if (null == obj || obj.IsReference)
        continue;

      if (color != obj.Attributes.ObjectColor)
      {
        obj.Attributes.ObjectColor = color;
        obj.Attributes.ColorSource = Rhino.DocObjects.ObjectColorSource.ColorFromObject;
        obj.CommitChanges();
      }
    }

    doc.Views.Redraw();

    return Rhino.Commands.Result.Success;
  }
}
```
{: #cs .tab-pane .fade .in .active}


```vbnet
Partial Friend Class Examples
  Public Shared Function ObjectColor(ByVal doc As Rhino.RhinoDoc) As Rhino.Commands.Result
	Dim objRefs() As Rhino.DocObjects.ObjRef = Nothing
	Dim cmdResult As Rhino.Commands.Result = Rhino.Input.RhinoGet.GetMultipleObjects("Select objects to change color", False, Rhino.DocObjects.ObjectType.AnyObject, objRefs)
	If cmdResult IsNot Rhino.Commands.Result.Success Then
	  Return cmdResult
	End If

	Dim color As System.Drawing.Color = System.Drawing.Color.Black
	Dim rc As Boolean = Rhino.UI.Dialogs.ShowColorDialog(color)
	If Not rc Then
	  Return Rhino.Commands.Result.Cancel
	End If

	For i As Integer = 0 To objRefs.Length - 1
	  Dim obj As Rhino.DocObjects.RhinoObject = objRefs(i).Object()
	  If Nothing Is obj OrElse obj.IsReference Then
		Continue For
	  End If

	  If color <> obj.Attributes.ObjectColor Then
		obj.Attributes.ObjectColor = color
		obj.Attributes.ColorSource = Rhino.DocObjects.ObjectColorSource.ColorFromObject
		obj.CommitChanges()
	  End If
	Next i

	doc.Views.Redraw()

	Return Rhino.Commands.Result.Success
  End Function
End Class
```
{: #vb .tab-pane .fade .in}


```python
# No Python sample available
```
{: #py .tab-pane .fade .in}

