---
title: Determine Object Layer
description: Demonstrates how to determine which layer a user-specified object is on and print the name.
authors: ['steve_baer']
author_contacts: ['stevebaer']
sdk: ['RhinoCommon']
languages: ['C#', 'Python', 'VB']
platforms: ['Windows', 'Mac']
categories: ['Adding Objects', 'Layers']
origin: http://wiki.mcneel.com/developer/rhinocommonsamples/objectlayer
order: 1
keywords: ['determine', 'objects', 'layer']
layout: code-sample-rhinocommon
---

```cs
partial class Examples
{
  public static Rhino.Commands.Result DetermineObjectLayer(Rhino.RhinoDoc doc)
  {
    Rhino.DocObjects.ObjRef obref;
    Rhino.Commands.Result rc = Rhino.Input.RhinoGet.GetOneObject("Select object", true, Rhino.DocObjects.ObjectType.AnyObject, out obref);
    if (rc != Rhino.Commands.Result.Success)
      return rc;
    Rhino.DocObjects.RhinoObject rhobj = obref.Object();
    if (rhobj == null)
      return Rhino.Commands.Result.Failure;
    int index = rhobj.Attributes.LayerIndex;
    string name = doc.Layers[index].Name;
    Rhino.RhinoApp.WriteLine("The selected object's layer is '{0}'", name);
    return Rhino.Commands.Result.Success;
  }
}
```
{: #cs .tab-pane .fade .in .active}


```vbnet
Partial Friend Class Examples
  Public Shared Function DetermineObjectLayer(ByVal doc As Rhino.RhinoDoc) As Rhino.Commands.Result
	Dim obref As Rhino.DocObjects.ObjRef = Nothing
	Dim rc As Rhino.Commands.Result = Rhino.Input.RhinoGet.GetOneObject("Select object", True, Rhino.DocObjects.ObjectType.AnyObject, obref)
	If rc IsNot Rhino.Commands.Result.Success Then
	  Return rc
	End If
	Dim rhobj As Rhino.DocObjects.RhinoObject = obref.Object()
	If rhobj Is Nothing Then
	  Return Rhino.Commands.Result.Failure
	End If
	Dim index As Integer = rhobj.Attributes.LayerIndex
	Dim name As String = doc.Layers(index).Name
	Rhino.RhinoApp.WriteLine("The selected object's layer is '{0}'", name)
	Return Rhino.Commands.Result.Success
  End Function
End Class
```
{: #vb .tab-pane .fade .in}


```python
import Rhino
import scriptcontext
import System.Guid

def DetermineObjectLayer():
    rc, obref = Rhino.Input.RhinoGet.GetOneObject("Select object", True, Rhino.DocObjects.ObjectType.AnyObject)
    if rc!=Rhino.Commands.Result.Success: return rc
    rhobj = obref.Object()
    if rhobj is None: return Rhino.Commands.Result.Failure
    index = rhobj.Attributes.LayerIndex
    name = scriptcontext.doc.Layers[index].Name
    print "The selected object's layer is '", name, "'"
    return Rhino.Commands.Result.Success

if __name__ == "__main__":
    DetermineObjectLayer()
```
{: #py .tab-pane .fade .in}
