===================================
File Navigation and File Management
===================================

Sublime Text includes a variety of features
to help you keep your work organized
and find your way around your projects.

.. contents::
    :local:
    :depth: 2

.. _fm-goto-anything:

Goto Anything
=============

Use Goto Anything
to **navigate your project's files** swiftly.
(More about projects later.)

.. image:: file-management-goto-anything.png

To open Goto Anything,
press :kbd:`Ctrl+P`.
As you type into the input area,
names of files in the current project
will be searched,
and a preview of the best match
will be shown.
This preview is *transient*;
that is, it won't become the actual active view
until you perform some operation on it.
Transient views go away when you press :kbd:`Esc`.
You will find transient views in other situations,
for example when single-clicking a file on the sidebar.

Goto Anything lives up to its name
--there's more to it than locating files.


Goto Anything Operators
-----------------------

Goto Anything understands several operators.
All of them can be used
on their own or after the search term.

Example::

	models:123

This instructs Sublime Text
to first search for a file
that matches ``models``,
and then to go to line 123 in that file.


Supported Operators
^^^^^^^^^^^^^^^^^^^

.. _fm-goto-symbol:

:samp:`@{symbol}`
    Searches for the symbol named ``symbol``
    in the active file.

    Symbols usually include classes and functions,
    but can in fact extract names
    from any scope declared
    in the corresponding syntax definition.
    If no symbols are defined
    for the active file type,
    the search will simply fail.

    .. note::

        Searching for symbols will only work
        if the active file type
        has symbols defined for it.
        Symbols are defined in ``.tmLanguage`` files.
        For more information about symbols,
        see :doc:`../reference/symbols`.

..    See *Symbols - Syntax Preferences*
..    (TODO: to be added).

:samp:`#{term}`
    Performs a fuzzy search of the ``term`` search term
    and highlights all matches.

:samp:`:{line_number}`
    Goes to the specified line number
    or to the end of the file
    (for numbers larger than the file's line count).

The Goto Anything operators
are bound to the following shortcuts:

+-----------------------+----------+
| Ctrl + R              | **@**    |
+-----------------------+----------+
| Ctrl + ;              | **#**    |
+-----------------------+----------+
| Ctrl + G              | **:**    |
+-----------------------+----------+

.. _fm-sidebar:

Sidebar
=======

The sidebar provides an overview
of the active project.
Files and folders in the sidebar
will be available in `Goto Anything`_
and project-wide actions
(like project-wide searches).

Projects and the sidebar are closely related.
It's important to note
that there's always an active project,
whether it's explicit or implicit.

The sidebar provides basic file management operations
through its context menu.

These are common shortcuts
related to the side bar:

+-----------------------+-----------------------------------------------------------+
| Ctrl + K, Ctrl + B    | Toggle side bar.                                          |
+-----------------------+-----------------------------------------------------------+
| Ctrl + 0              | Give the focus to the side bar.                           |
+-----------------------+-----------------------------------------------------------+
| Esc                   | Return the focus to the view.                             |
+-----------------------+-----------------------------------------------------------+
| Arrow keys            | Navigate side bar.                                        |
+-----------------------+-----------------------------------------------------------+

Files opened from the sidebar
create *semi-transient* views.
Unlike transient views, semi-transient views
show up as a new tab.
The tab title of semi-transient views appears in italics.
Before a new semi-transient view is opened,
any existing semi-transient view in the same pane
gets automatically closed.

Here's an example showing a normal view, a transient view,
and a semi-transient view.
Notice that the transient view has no tab:

.. image:: file-management-transient-views-detail.png

.. _fm-projects:

Projects
========

Projects group sets of files and folders
to keep your work organized.

There is always an active project.
If you haven't created one,
an implicit one is created by Sublime Text.

Set up a project by adding folders in a way
that suits you,
and then save your new configuration.

.. _fm-projects-folders:

You can add and remove folders to/from a project
using the **Project** menu
or the side bar's context menu.
If you drag a folder onto a Sublime Text window,
it will be added to the project too.

To save a project,
go to **Project → Save Project As...**.

To switch projects quickly,
press :kbd:`Ctrl+Alt+P`.
Using the menu,
you can select **Projects → Recent Projects**.

Project metadata is stored in JSON files
with a ``.sublime-project`` extension.
Wherever there's a ``.sublime-project`` file,
you will find an ancillary ``.sublime-workspace`` file too.
The second one is used by Sublime Text
and you shouldn't edit it.
(More on workspaces later.)

Projects can define settings applicable to that project only.
See the `official documentation`_ for more information.

.. _official documentation: http://www.sublimetext.com/docs/2/projects.html

.. TODO add settings example here.

You can open a project from the **command line**
by passing the ``.sublime- project`` file as an argument
to the ``subl`` command line helper
included with Sublime Text.

.. warning::

    A ``.sublime-project`` file is generally apt
    to be committed to a source code repository,
    but always be mindful of what you store in it.


The ``.sublime-project`` Format
-------------------------------

Project metadata in ``.sublime-project`` files
is split across three topmost sections:
``folders``, for the included folders; ``settings``,
for project-specific settings;
and ``build_systems``, for project-specific build systems.

.. code-block:: javascript
    :emphasize-lines: 2,14,18

    {
        "folders":
        [
            {
                "path": "src",
                "folder_exclude_patterns": ["backup"]
            },
            {
                "path": "docs",
                "name": "Documentation",
                "file_exclude_patterns": ["*.css"]
            }
        ],
        "settings":
        {
            "tab_size": 8
        },
        "build_systems":
        [
            {
                "name": "List",
                "cmd": ["ls"]
            }
        ]
    }


**Folder Options**

``path``
    Required.
    The path may be relative to the project directory,
    or absolute.

``folder_exclude_patterns``
    Optional. List of wildcards.
    Folders matching the wildcards will be excluded from the project.

``folder_include_patterns``
    Optional. List of wildcards.
    Folders matching the wildcards will be included in the project.

``file_exclude_patterns``
    Optional. List of wildcards.
    Files matching the wildcards will be excluded from the project.

``file_include_patterns``
    Optional. List of wildcards.
    Files matching the wildcards will be included in the project.

``name``
    Optional. If present, it will appear in the side bar.

.. TODO: there are more settings supported by projects.

**Settings**
    A project may define project-specific settings
    that will only apply to files within that project.
    Project-specific settings override user settings,
    but not syntax-specific settings.

    Almost all settings can be overridden
    (excluding global settings).

    .. seealso::

        :ref:`settings-hierarchy`
            A detailed example for the order of precedence for settings.
        :doc:`Settings - Reference </reference/settings>`
            Reference of available settings.

**Build Systems**
    You can define project-specific build systems
    in a ``.sublime-project`` file.
    A ``name`` must be specified for each one.
    Build systems included in a ``.sublime-project`` file
    will show up in the **Tools → Build Systems** menu.

    .. seealso::

        :doc:`Build Systems - Reference </reference/build_systems>`
            Documentation on build systems and their options.


Other Settings Related to the Sidebar and Projects
==================================================

``binary_file_patterns``
    A list of wildcards.
    Files matching these wildcards will show up in the side bar,
    but will be excluded from Goto Anything
    and Find in Files.

.. TODO: binary_file_patterns also applies to projects, right?

Workspaces
==========

Workspaces can be seen as different *views*
into the same project.
For example, you may want
to have only a few selected files open
while working on some feature.
Or perhaps you use a different pane layout
when you're writing tests, etc.
Workspaces help in these situations.

Workspaces behave very much like projects.
To create a new workspace,
select **Project → New Workspace for Project**.
To save the active workspace,
select **Project → Save Workspace As...**.

Workspaces data is stored in JSON files
with the *.sublime-workspace* extension.

To switch between different workspaces,
use :kbd:`Ctrl+Alt+P`,
exactly as you do with projects.

Workspaces data is stored in JSON files
with the ``.sublime-workspace`` extension.

Unlike ``.sublime-project`` files,
``.sublime-workspace`` files
are not meant to be shared or edited manually.
You should never commit ``.sublime-workspace`` files
into a source code repository.

As with projects, you can open a workspace
from the **command line**
by passing the desired ``.sublime-workspace`` file
as an argument to the ``subl`` command line helper
included with Sublime Text.

.. warning::
    Unlike ``.sublime-project`` files,
    ``.sublime-workspace`` files
    are not meant to be shared or edited manually.
    You should never commit ``.sublime-workspace`` files
    into a source code repository.


Panes
=====

Panes are groups of views.
In Sublime Text, you can have
multiple panes open at the same time.

You can manipulate panes
using default keyboard shortcuts:

+-----------------------+--------------------+
| Ctrl+K, Ctrl+↑        | Create new pane    |
+-----------------------+--------------------+
| Ctrl+K, Ctrl+↓        | Close active pane  |
+-----------------------+--------------------+

Further pane management commands
can be found under **View → Layout**
and related submenus.
