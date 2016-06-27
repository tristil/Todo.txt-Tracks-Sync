What Is It?
-----------

This is a plugin for the `todo.txt bash script <http://todotxt.com>`_
todo-management bash script that synchronizes a local todo.txt store with a
remote (`Tracks web app <https://github.com/TracksApp/tracks>`_) todo store.

This plugin depends on the  
`todo.txt-python library <https://github.com/tristil/todo.txt-python>`_ and
the `tracks-python library <https://github.com/tristil/tracks-python>`_. The reason
for using Python for this integration was to be able to run the syncing plugin
on a standard Linux server where the user doesn't have any installation
privileges.

Installation
------------
todo.txt-python and tracks-python are included as Git subprojects. To fetch them
clone a copy of the plugin in your todo.txt addons directory (by default is ``~/.todo.actions.d`` but check your ``todo.cfg`` file).
If this directory doesn't exists, create it and then fetch the subprojects by
using the submodule commands:::

  cd ~/.todo.actions.d
  git clone https://github.com/tristil/Todo.txt-Tracks-Sync.git tracks-sync
  cd tracks-sync
  git submodule init
  git submodule update
  cd ..
  ln -s tracks-sync/tsync
  chmod +x tsync

It's that easy! But wait, there's more! Add these values to the top of your ``todo.cfg`` file:::

  export TRACKS_URL="http://tracks.example.com"
  export TRACKS_USERNAME="username"
  export TRACKS_PASSWORD="password"
  
Check if the values of ``todo_dir``, ``todo_file``, ``done_file``, ``report_file`` and ``todo_actions_dir`` are right in the file ``tracks-sync/todotxt/parser.py``

Then you should be able to run the tsync command as add-on of ``todo.sh`` (we assume ``t`` is an alias of your ``todo.sh``):::

  t tsync

Notes
-----
I would say at the moment that this plugin is a bit rough. If you use this with
your "production" todo.txt or Tracks installation, you should BACKUP both of
them. 

Major caveats for using this plugin are:

* It may not see much more active development.
* When it's working correctly it will append a tid: keyword to every todo,
  associating the local store with an todos id from the remote store.
* It guesses that when a remote todo does not appear in the feed of active
  todos that it is completed. It therefore will do the wrong thing when a todo
  is deleted or deferred. This is done because typically the feed of done items
  is too long to compare against until a search api is built.


Feedback
--------
If somebody actually has a use for this plugin and has additional
requirements/ bugs / patches, go ahead and submit them as Github issues and I
will respond to them as quickly as possible.
