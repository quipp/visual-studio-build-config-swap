# Visual Studio Build Config Swap

Trick for getting Visual Studio projects to swap configuration files based on selected Build.  This strategy is  useful for non-Web Projects - because they don't have a good system for this yet in VS 2013.  However, a better solution would be to use a Build tool like Grunt or Gulp - which is what's encouraged for VS 2015.

Visual Studio 2013 added support for unlimited Publish Profiles for Web Sites with Web.config tranforms for each publish profile.  Just create a publish profile for each tranform file, then right-click on the *.pubxml file and select the menu item to Add Config Transform.  This strategy can still be useful for WinForm's applications (non-Web projects).

This was tested with Visual Stuidio 2013 (& 2010 a few years ago).

The is based on a combination of strategies from the following two sites
http://geekswithblogs.net/SoftwareDoneRight/archive/2010/01/30/how-to-get-pre-build-event-support-for-web-site-projects.aspx
http://stackoverflow.com/questions/2382826/managing-a-debug-and-release-connection-string

The key is to use *Build Event* which uses *MSBuild* script to *swap one web config into web.config* based on the currently *selected build configuration*.  Another trick is to include *a library project* in solution, because those support Build Events (Web Sites do NOT).  The library project's Build Events is used to kick off the web.config copy.

**Must Rebuild to ensure the build events happen** (if Build and no change has occured in library project, it won't build and therefore wont perform web config swap).

