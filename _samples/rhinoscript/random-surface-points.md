---
title: Random Surface Points
description: Generate random points on a surface using RhinoScript.
authors: ['dale_fugier']
author_contacts: ['dale']
sdk: ['RhinoScript']
languages: ['VBScript']
platforms: ['Windows']
categories: ['Adding Objects', 'Surfaces']
origin: http://wiki.mcneel.com/developer/scriptsamples/randomsurfacepoints
order: 1
keywords: ['rhinoscript', 'vbscript']
layout: code-sample-rhinoscript
---

```vbnet
Sub RandomSurfacePoints()

  Dim srf, num, cnt
  Dim dom_u, dom_v, uv(1), pt

  srf = Rhino.GetObject("Select surface", 8, True, True)
  If IsNull(srf) Then Exit Sub

  num = Rhino.GetInteger("Number of points", 10, 1)
  If IsNull(num) Then Exit Sub

  Call Rhino.EnableRedraw(False)

  Randomize
  dom_u = Rhino.SurfaceDomain(srf, 0)
  dom_v = Rhino.SurfaceDomain(srf, 1)
  cnt = 0

  While (cnt < num)
    uv(0) = Rnd() * (dom_u(1) - dom_u(0)) + dom_u(0)
    uv(1) = Rnd() * (dom_v(1) - dom_v(0)) + dom_v(0)
    pt = Rhino.EvaluateSurface(srf, uv)
    If (Rhino.IsPointOnSurface(srf, pt) = True) Then
      Call Rhino.AddPoint(pt)
      cnt = cnt + 1
    End If
  Wend

  Call Rhino.EnableRedraw(True)

End Sub
```
