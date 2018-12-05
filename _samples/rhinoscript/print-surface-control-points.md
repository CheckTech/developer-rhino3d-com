---
title: Print Surface Control Points
description: Demonstrates how to print the location of a surface's control points using RhinoScript.
authors: ['dale_fugier']
author_contacts: ['dale']
sdk: ['RhinoScript']
languages: ['VBScript']
platforms: ['Windows']
categories: ['Surfaces']
origin: http://wiki.mcneel.com/developer/scriptsamples/printsurfacepoints
order: 1
keywords: ['rhinoscript', 'vbscript']
layout: code-sample-rhinoscript
---

```vbnet
Option Explicit

Sub PrintSurfacePoints

Dim strSurface
strSurface = Rhino.GetObject("Select surface", 8)
If IsNull(strSurface) Then Exit Sub  

Dim arrPoints
arrPoints = Rhino.SurfacePoints(strSurface)
If Not IsArray(arrPoints) Then Exit Sub

Dim arrCount
arrCount = Rhino.SurfacePointCount(strSurface)

Dim u, v
Dim ulast : ulast = arrCount(0)
Dim vlast : vlast = arrCount(1)
Dim i : i = 0

For u = 0 To ulast - 1
  For v = 0 To vlast - 1
    Rhino.Print "CV[" & CStr(u) & "," & CStr(v) & "] = " _
          & Rhino.Pt2Str(arrPoints(i), 3)
    i = i + 1
  Next
Next

End Sub
```
