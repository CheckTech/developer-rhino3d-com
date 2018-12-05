---
title: Generating Random Numbers
description: This guide demonstrates how to generate random numbers that fall within a specified range using RhinoScript.
authors: ['dale_fugier']
author_contacts: ['dale']
sdk: ['RhinoScript']
languages: ['VBScript']
platforms: ['Windows']
categories: ['Miscellaneous', 'Intermediate']
origin: http://wiki.mcneel.com/developer/scriptsamples/randomnumber
order: 1
keywords: ['script', 'Rhino', 'vbscript']
layout: toc-guide-page
---

 
## Standard VBScript

The following code sample demonstrates how to generate random integers that fall within a specified range.

First, the standard VBScript method:

```vbnet
Sub Test1()
  nLow = 1
  nHigh = 100
  Randomize
  Rhino.Print Int((nHigh - nLow + 1) * Rnd + nLow)
End Sub
```

**NOTE**: since the `Int` function always rounds down, we add one to the difference between the limits.

## Using .NET

Now, a little help from the .NET Framework:

```vbnet
Sub Test2()
  nLow = 1
  nHigh = 100
  Set objRandom = CreateObject("System.Random")
  Rhino.Print objRandom.Next_2(nLow, nHigh)
End Sub
```

## Floating Point

If you want a random floating point number that falls within a specified range, you can use the technique below...

```vbnet
Sub Test3()
  dblLow = 10.0
  dblHigh = 50.0
  Randomize
  Rhino.Print Rnd * (dblHigh - dblLow) + dblLow
End Sub
```
