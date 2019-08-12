---
title: Pick Angle Interactively
description: Demonstrates how to use the CRhinoGetAngle class to pick an angle.
authors: ['dale_fugier']
sdk: ['C/C++']
languages: ['C/C++']
platforms: ['Windows']
categories: ['Picking and Selection']
origin: http://wiki.mcneel.com/developer/sdksamples/getangle
order: 1
keywords: ['rhino']
layout: code-sample-cpp
---

```cpp
CRhinoCommand::result CCommandTest::RunCommand(const CRhinoCommandContext& context)
{
  // Prompt for base point
  CRhinoGetPoint gp;
  gp.SetCommandPrompt( L"Base point" );
  gp.ConstrainToConstructionPlane( FALSE );
  gp.GetPoint();
  if( gp.CommandResult() != CRhinoCommand::success )
    return gp.CommandResult();

  // Get first picked point
  ON_3dPoint origin = gp.Point();

  // Get view used during GetPoint
  CRhinoView* view = gp.View();
  if( !view )
  {
    // If scripted, get active view
    view = ::RhinoApp().ActiveView();
    if( !view )
      return CRhinoCommand::failure;
  }

  // Get view's construction plane and move it to the picked point
  ON_Plane plane = view->Viewport().ConstructionPlane().m_plane;
  plane.SetOrigin( origin );

  // Prompt for first reference point
  gp.SetCommandPrompt( L"First reference point" );
  gp.SetBasePoint( origin );
  gp.DrawLineFromPoint( origin, TRUE );
  gp.Constrain( plane );  // Constrain picking to plane
  gp.GetPoint();
  if( gp.CommandResult() != CRhinoCommand::success )
    return gp.CommandResult();

  // Get second picked point
  ON_3dPoint refpt = gp.Point();

  // Prompt for angle
  CRhinoGetAngle ga;
  ga.SetCommandPrompt( L"Second reference point" );
  ga.SetBasePoint( origin );
  ga.SetBase( origin );
  ga.SetReferencePoint( refpt );
  ga.Constrain( plane );  // Constrain picking to plane
  ga.GetAngle();
  if( ga.CommandResult() != CRhinoCommand::success )
    return ga.CommandResult();

  // Results
  double radians = ga.Angle();
  double degrees = radians * (180.0/ON_PI);
  RhinoApp().Print( L"Angle = %f.\n", degrees );

  return CRhinoCommand::success;
}
```
