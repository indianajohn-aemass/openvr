Random notes
------------

* To compile this example in MacOSX, you must install brew and type:

````
brew install sdl2
````

* Steam must be installed and running to execute anything.

* You must set DYLIB_LIBRARY_PATH in order to run the example.

````
DYLD_LIBRARY_PATH=/Users/aemass/dev/openvr/lib/osx32/:/Applications/Steam.app/Contents/MacOS/:${DYLD_LIBRARY_PATH} ./hellovr_opengl
````
