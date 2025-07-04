Changelog
=========

3.2
---

Geometric Modelling Kernel (NURBS)

* Improve the difference boolean operations.
* Extrude groups have a checkbox to allow skewing - 3 DoF for the extrude direction.

Constraints (new and improved):

* Add Parallel and Perpendicular constraints for 2 faces.
* The equal angle constraint is moved to the `N` shortcut and menu item to allow equal length (`Q`) to be applied to three or four lines.
* Allow tangent on arcs/lines/splines without coincident endpoints.

Allow these constraints to be applied to more entities at once:

* More than two line Segments - equal length.
* More than two Arcs and/or circles - equal diameter/radius.
* Any number of Lines - horizontal or vertical.
* More than two points - horizontal or vertical.
* Point on face can be applied to a point and 1-3 faces at once.
* More than two points coincident.

Sketching

* `Image` sketch elements are not copied in 3d groups (extrude, lathe, revolve, helix) by default. `Toggle Construction` for an image to get the old behavior.
* New option to use radius instead of diameter for circle and arc dimensions.
* Dimensions on arcs default to radius instead of diameter. Uncheck `use radius` in the Property Browser to get diameters.
* `Text in True Type Font` elements now support basic kerning. Enable it with `apply kerning` in the Property Browser.

Translations (now in 10 languages!)

* Added Czech  cs_CZ.
* Added Japanese ja_JP.
* Update translation for French fr_FR, Russian ru_RU, Chinese zh_CN and Ukrainian uk_UA.

Other User interface changes:

* `CTRL+Tab` hides/shows the toolbar.
* Marquee selection of line segments is now precise.
* Speed up the animation when moving the view, for example when pressing `F2` or `F3`.
* Pressing ESC while drawing a sketch entity now deletes the entity rather than completing it.
* `CTRL+Shift+S` shortcut for "Save As..."
* New option "use camera mouse navigation" for camera (instead of the default model) rotation navigation.
* Sketches can be displayed with only dimensions visible (the button controlling visibility of constraints in the Property Browser has a new state).
* More entity types described in the text screens.
* A new option to `display the full path in the title bar`; or not.
* Handle smooth scrolling (mouse wheel zoom) on GTK/Linux.
* The embedded vector font (used for the UI and labels):
	* now has many new and improved Chinese characters
	* includes the Greek alphabet
	* improved "є"
	* added superscript 5 "⁵"
	* fixed crash when typing "£"
* The animation speed when changing the 3D view is configurable.
* Add an 'only unconstrained' option on the Property Browser home screen that shows only unconstrained groups.


Other

* STEP files export as solid model(s).
* Merged and improved the experimental Web version (Emscripten port).
* Better Flatpack support.
* Several bug fixes and usability improvements.
* Allow 32 bit SolveSpace to access up to 4GB of RAM to allow working on larger projects.

Bug fixes:

* `Paste Transformed` on elements that contain a point-line distance does not flip any more.
* Fix saving assemblies when opened with a relative path on the command line.
* Windows: The Property Browser remains visible when going full screen (CTRL-F11).
* Fix crash when linking .STL and .EMN files with extensions in capital letters.
* Mac: Don't crash on file ops without changing dir.
* Fix incorrect arc handling when linking IDF files.
* Windows: avoid (sometimes) showing multiple messages when deleting an entity causes other entities to be removed.

3.1
---

Constraints:

* Arcs length ratio and difference.
* Arc & Line length ratio and difference.
* Allow comments to be associated with point entities.

Sketching:

* Support for pan, zoom and rotate trackpad gestures on macOS
* Add "exploded view" to sketches via "\\" key. Shows sketch elements separated
  by a configurable distance perpendicular to the sketch plane.
* Added Feet-Inches as a unit of measure. Inputs are still in inches.
  But the display shows feet, inches, and fraction of an inch.
* Added an optional "pitch" parameter to helix extrusions (in the text window)
* Allow use of Point & Normal to define "sketch-in-new-workplane".
* Update "Property Browser" live while dragging the sketch.

MISC:

* Add a link to the GitHub commit from which SolveSpace was built in the Help
  menu.
* Make all points, vectors and normals shown in the Property Browser into
  active links. This makes them explorable and selectable.
* Load 16bit PNG images correctly by re-scaling to 8bit.
* Fixed hang when trying to display characters missing from the embedded font.
* The main window vertical size can be as small as the toolbar.
* Configurable "SafeHeight" parameter instead of the fixed 5mm for G-code export.
* Add Spanish / Argentina translation.
* Move "perspective factor", "lighting direction" and "explode distance" from
  the "configuration" screen to the "view" screen.
* Add a "∆" suffix to groups which have "force to triangle mesh" ticked
* Gray the group name in the text window for groups with suppressed solid model.
* Added the ability to Link STL files.
* When linking circuit boards (IDF .emn files) show keepout regions as construction entities.

Performance:

* Speed up sketches with many constraints by roughly 8x by using the Eigen
  library in the solver. The maximum unknowns increased from 1024 to 2048.
* Add a "suppress dof calculation" setting to groups - increases performance for
  complex sketches.
* More changes to the ID list implementation.

3.0
---

New sketch features:

* New intersection boolean operation for solid models.
* New groups, revolution and helical extrusion.
* Extrude, lathe, translate and rotate groups can use the "assembly"
  boolean operation, to increase performance.
* The solid model of extrude and lathe groups can be suppressed,
  for splitting a single model in multiple parts to export,
  or if only the generated entities are desired, without the mesh.
* Translate and rotate groups can create n-dimensional arrays using
  the "difference" and "assembly" boolean operations.
* A new sketch in workplane group can be created based on existing workplane.
* TTF text request has two additional points on the right side, which allow
  constraining the width of text.
* Image requests can now be created, similar to TTF text requests.
  This replaces the "style → background image" feature.
* Irrelevant points (e.g. arc center point) are not counted when estimating
  the bounding box used to compute chord tolerance.
* When adding a constraint which has a label and is redundant with another
  constraint, the constraint is added as a reference, avoiding an error.
* Datum points can be copied and pasted.
* "Split Curves at Intersection" can now split curves at point lying on curve,
  not just at intersection of two curves.
* Property browser now shows amount of degrees of freedom in group list.
  It also shows a yellow "err" if the sketch has problems (e.g. self
  intersecting) that would propagate in subsequent groups.
* It is now possible to press "g" to toggle construction on new objects while
  they are still being drawn.
* Allow right click to end sketching of all entities.

New constraint features:

* When dragging an arc or rectangle point, it will be automatically
  constrained to other points with a click.
* When selecting a constraint, the requests it constraints can be selected
  in the text window.
* When selecting an entity, the constraints applied to it can be selected
  in the text window.
* Distance constraint labels can now be formatted to use SI prefixes.
  Values are edited in the configured unit regardless of label format.
* When creating a constraint, if an exactly identical constraint already
  exists, it is now selected instead of adding a redundant constraint.
* It is now possible to turn off automatic creation of horizontal/vertical
  constraints on line segments.
* Automatic creation of constraints no longer happens if the constraint
  would have been redundant with other ones.
* New option to open the constraint editor for newly created constraints
  with a value.
* New "redundant constraint timeout (in ms)" option to prevent UI freeze
  when looking for redundant constraints.
* Swap vertical and horizontal constraints when pasting rotated by 90/270
  degrees.

New export/import features:

* Link IDF circuit boards in an assembly (.emn files)
* Three.js: allow configuring projection for exported model, and initially
  use the current viewport projection.
* Wavefront OBJ: a material file is exported alongside the model, containing
  mesh color information.
* DXF/DWG: 3D DXF files are imported as construction entities, in 3d.
* VRML (WRL) triangle meshes can now be exported, useful for e.g. [KiCAD](http://kicad.org).
* Export 2d section: custom styled entities that lie in the same
  plane as the exported section are included.
* Added ExportBackgroundColor in configuration for EPS, PDF, and SVG files.
* STEP export includes object colors and transparency.
* Default "line styles" have a new "export these objects" option.

New rendering features:

* The "Show/hide hidden lines" button is now a tri-state button that allows
  showing all lines (on top of shaded mesh), stippling occluded lines
  or not drawing them at all.
* The "Show/hide outlines" button is now independent from "Show/hide edges".
* "View | Darken Inactive Solids" added. When turned off and a "sketch in plane"
  group is active solids form previous groups will not be "darkened" (have the
  s000d-#def-dim-solid style applied to them).

New measurement/analysis features:

* New choice for base unit, meters.
* New command for measuring total length of selected entities,
  "Analyze → Measure Perimeter".
* New command for measuring center of mass, with live updates as the sketch
  changes, "Analyze → Center of Mass".
* New option for displaying areas of closed contours.
* When calculating volume of the mesh, volume of the solid from the current
  group is now shown alongside total volume of all solids.
* When calculating area, and faces are selected, calculate area of those faces
  instead of the closed contour in the sketch.
* When selecting a point and a line, projected distance to current
  workplane is displayed.

Other new features:

* Improvements to the text window for selected entities and constraints.
* Ambient light source added in text window to allow flat shaded renderings.
* New command-line interface, for batch exporting and more.
* The graphical interface now supports HiDPI screens on every OS.
* New option to lock Z axis to be always vertical when rotating the view,
  a.k.a. "turntable navigation".
* New button to hide all construction entities.
* New link to match the on-screen size of the sketch with its actual size,
  "view → set to full scale".
* When zooming to fit, constraints are also considered.
* Ctrl-clicking entities now deselects them, as the inverse of clicking.
* When clicking on an entity that shares a place with other entities,
  the entity from the current group is selected.
* When dragging an entity that shares a place with other entities,
  the entity from a request is selected. For example, dragging a point on
  a face of an extrusion coincident with the source sketch plane will
  drag the point from the source sketch.
* The default font for TTF text is now Bitstream Vera Sans, which is
  included in the resources such that it is available on any OS.
* In expressions, numbers can contain the digit group separator, "_".
* The "=" key is bound to "Zoom In", like "+" key.
* The numpad decimal separator key is bound to "." regardless of locale.
* On Windows, full-screen mode is implemented.
* On Linux, native file chooser dialog can be used.
* New edit menu items "Line Styles", "View Projection" and "Configuration"
  that are shortcuts to the respective configuration screens.
* New cmake build options using -DENABLE_OPENMP=yes and -DENABLE_LTO=yes
  to enable support for multi-threading and link-time optimization.
* "Shift+Scroll" for ten times finer zoom.
* Translations: Chinese, French, German, Russian, Turkish, Ukrainian.

Bugs fixed:

* Fixed broken --view options for command line thumbnail image creation.
* Some errors in Triangulation of surfaces.
* Some NURNS boolean operations that failed particularly on surfaces
  created with Lathe, Revolve, or Helix.
* Segfault in Remove Spline Point context menu.
* A point in 3d constrained to any line whose length is free no longer
  causes the line length to collapse.
* Curve-line constraints (in 3d), parallel constraints (in 3d), and
  same orientation constraints are more robust.
* Adding some constraints (vertical, midpoint, etc) twice errors out
  immediately, instead of later and in a confusing way.
* Constraining a newly placed point to a hovered entity does not cause
  spurious changes in the sketch.
* Points highlighted with "Analyze → Show Degrees of Freedom" are drawn
  on top of all other geometry.
* A step rotate/translate group using a group forced to triangle mesh
  as a source group also gets forced to triangle mesh.
* Paste Transformed with a negative scale does not invert arcs.
* The tangent arc now modifies the original entities instead of deleting
  them, such that their constraints are retained.
* When linking a sketch file, missing custom styles are now imported from
  the linked file.
* 3Dconnexion SpaceMouse should now work (on Windows and macOS X).
* Improved NURBS boolean operations on curved surfaces in some cases.
* Show only usable fonts in the font selector.

2.x
---

Bug fixes:

* Do not crash when changing an unconstrained lathe group between
  union and difference modes.

2.3
---

Bug fixes:

* Do not crash when applying a symmetry constraint to two points.
* Fix TTF font metrics again (properly this time).
* Fix the "draw back faces in red" option.
* Fix export of wireframe as 3D DXF.
* Various minor crashes.

2.2
---

Other new features:

* OS X: support 3Dconnexion devices (SpaceMouse, SpaceNavigator, etc).
* GTK: files with uppercase extensions can be opened.

Bug fixes:

* Do not remove autosaves after successfully opening a file, preventing
  data loss in case of two abnormal terminations in a row.
* Do not crash when changing autosave interval.
* Unbreak the "Show degrees of freedom" command.
* Three.js: correctly respond to controls when browser zoom is used.
* OS X: do not completely hide main window when defocused.
* GTK: unbreak 3Dconnexion support.
* When pasting transformed entities, multiply constraint values by scale.
* Fix TTF font metrics (restore the behavior from version 2.0).
* Forcibly show the current group once we start a drawing operation.
* DXF export: always declare layers before using them.
* Do not truncate operations on selections to first 32 selected entities.
* Translate and rotate groups inherit the "suppress solid model" setting.
* DXF: files with paths containing non-ASCII or spaces can be exported
  or imported.
* Significantly improved performance when dragging an entity.
* Various crashes and minor glitches.

2.1
---

New sketch features:

* Lathe groups create circle and face entities.
* New toolbar button for creating lathe groups.
* Chord tolerance is separated into two: display chord tolerance (specified
  in percents, relative to model bounding box), and export chord tolerance
  (specified in millimeters as absolute value).
* Bezier spline points can be added and removed after the spline is created.
* When an unconstrained extrusion is switched between "union" and
  "difference", its normal is flipped.
* Groups can be added in the middle of the stack. Note that this results
  in files incompatible with version 2.0.
* Active group can be removed.
* Removing an imported group does not cause all subsequent groups to also
  be removed.
* When a new group with a solid is created, the color is taken from
  a previous group with a solid, if any.
* Entities in a newly active group do not become visible.
* When entities are selected, "Zoom to fit" zooms to fit only these
  entities and not the entire sketch.
* Zero-length edges are reported with a "zero-length error", not
  "points not all coplanar".

New constraint features:

* Height of the font used for drawing constraint labels can be changed.
* New constraint, length difference, placed with J.
  (Patch by Peter Ruevski)
* Horizontal/vertical constraints are automatically added if a line segment
  is close enough to being horizontal/vertical. This can be disabled by
  holding Ctrl.
* Reference dimensions and angles can be placed with Shift+D and Shift+N.
* Copying and pasting entities duplicates any constraints that only involve
  entities in the clipboard, as well as selected comments.
* Diameter constraints can be shown as radius.
* The "pi" identifier can be used in expressions.
* Constraint labels can be snapped to grid.
* Integer angles are displayed without trailing zeroes.
* Angle constraints have proper reference lines and arrowheads.
* Extension lines are drawn for point-line distance constraints.

New solver features:

* Sketches with redundant and unsolvable constraints are distinguished.
* New group setting, "allow redundant constraints". Note that it makes
  the solver less stable.

New rendering and styling features:

* New line style parameter: stippling, based on ISO 128.
* Outlines of solids can be drawn in a particular style (by default, thick
  lines) controlled by the "Show outline of solid model" button.
* Occluded edges can be drawn in a particular style (by default, stippled
  with short dashes) controlled by the "Show hidden lines" button.
* Solids can be made transparent.

New export/import features:

* The old "import" command (for .slvs files) is renamed to "link".
* If a linked .slvs file is not found, first the relative path recorded
  in the .slvs file is checked and then the absolute path; this is
  an inversion of the previously used order. If it is still not found,
  a dialog appears offering to locate it.
* DXF and DWG files can be imported, with point-coincident, horizontal and
  vertical constraints automatically inferred from geometry, and distance
  and angle constraints created when a dimension placed against geometry
  exists.
* Triangle mesh can be exported for viewing in the browser through WebGL.
* Export dialogs remember the last file format used, and preselect it.
* Exported DXF files have exact circles, arcs and splines instead of
  a piecewise linear approximation (unless hidden line removal was needed).
* Exported DXF files preserve color and line thickness.
* In exported DXF files, constraints are represented as DXF dimensions,
  instead of piecewise linear geometry.
* When exporting 2d views, overlapping lines are removed.

Other new features:

* Native Linux (GTK 2 and GTK 3) and Mac OS X ports.
* Automatically save and then restore sketches if SolveSpace crashes.
  (Patch by Marc Britten)
* Unicode is supported everywhere (filenames, group names, TTF text,
  comments), although RTL scripts and scripts making heavy use of ligatures
  are not rendered correctly.
* The vector font is grid-fitted when rendered on screen to make it easier
  to read regardless of its size.

2.0
---

Initial public release.
