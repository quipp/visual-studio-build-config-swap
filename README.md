# aspnet-website-webconfig-swap
Trick for getting Visual Studio Web Sites to have unlimited web.config alternatives (pseudo transformations).  By default Web Sites only support one transform file (web.debug.config).  This gets around that.

This was tested with only Visual Stuidio 2013.

The is based on a combination of strategies from the following two sites
http://geekswithblogs.net/SoftwareDoneRight/archive/2010/01/30/how-to-get-pre-build-event-support-for-web-site-projects.aspx
http://stackoverflow.com/questions/2382826/managing-a-debug-and-release-connection-string

The key is to use *Build Event* which uses *MSBuild* script to *swap one web config into web.config* based on the currently *selected build configuration*.  Another trick is to include *a library project* in solution, because those support Build Events (Web Sites do NOT).  The library project's Build Events is used to kick off the web.config copy.

**Must Rebuild to ensure the build events happen** (if Build and no change has occured in library project, it won't build and therefore wont perform web config swap).

Again, this is just a hack to compensate for web site configuration limitations.  Could use Publish Profiles (but to get transofmations working, must use Web Deploy).  This solultion is more hacky, but does not require Web Deploy.

For yet another hacky solution to Web Site configuration limitations see https://github.com/quipp/visual-studio-web-site-config-transform-hack
