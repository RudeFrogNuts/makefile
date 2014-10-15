makefile
========

Working on general makefile for GNU gcc/g++ on Linux.  I couldn't find anything that would allow me to build a release and debug version in seperate directories and I wanted soemthing that would allow for seperate procesing of .c and .cpp files without using default gcc passthrough.  When the makefile is completed, I plan to write a couple of BASH scripts that I can use to setup new projects from the command line based on custom templates.  Finally, I hope to be able to autogenerate a .pro file so that the projects can also be opened in Qt.

What it does so far:

1. Uses following project tree:

project/src
project/inc
project/lib
project/bin
project/bin/release
project/bin/debug

2. Uses MAKECMDGOALS to set OBJDIR for release and debug but still builds the
binary in ./bin (for now).  This is just to separte the builds in future and
allow for debug and optimizaton defaults/targets.

3. Automatically loads and seperates object files from SRCDIR in OBJS for .c and .cpp.

4. Uses the proper compiler (CC, or CXX) for .c and .cpp object builds.

5. If mixing .c and .cpp object files, the target.exe build uses CXX.  if not,
the target.exe build uses proper compiler based on source files.

6. .c and .cpp object files are designated with .o (for .c) and .opp (for .cpp)
so that the correct compilre can be chosen via target based on source
extenstion.

7. Designated all .PHONY targets.

8. Added 'show' target to echo makefile variables for debuging.

9. Changed to $(RM) for platform independance.  Still working on other platform
dependency issues; but, I just use linux for now.

10. Added support for CPPFLAGS CXXFLAGS CFLAGS with debug/release logic.  You
can still pass values to these FLAGS via make and they will be combined with
standard project FLAGS specified in makefile.

11. Added LIBS and included in CC, CXX, CCC compiler options.  This must be set
based on project.  I did not include anything by default.

12. Considering LDLIBS and LDFLAGS.

13. Branched for Automatic Prerequisites of .h/.hpp in object builds.

Still working on/learning a number of pieces - this is far from complete.  I'm
testing and learning as I go.  Ultimately I want a makefile that will address
the vast majority of my projects on multiple platforms.
