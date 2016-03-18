# Kaggle_JuliaTutorial

Author: lapostoj

Contact: jerome.lapostolet@gmail.com

## Description
Code written while following this tutorial: https://www.kaggle.com/c/street-view-getting-started-with-julia

## Bug Fixes
### ImageMagick
* Message: 'ERROR: no decode delegate for this image format BMP'
* Solution: Replace content of 'deps.jl' (C:\Users\\[username]\\.julia\v0.4\ImageMagick\deps\) with
```
# This is an auto-generated file; do not edit
# Pre-hooks

# Macro to load a library
macro checked_lib(libname, path)
	((VERSION >= v"0.4.0-dev+3844" ? Base.Libdl.dlopen_e : Base.dlopen_e)(path) == C_NULL) && error("Unable to load \n\n$libname ($path)\n\nPlease re-run Pkg.build(package), and restart Julia.")
	quote const $(esc(libname)) = $path end
end

# Load dependencies
@checked_lib libwand "C:\\Program Files\\ImageMagick-6.9.3-Q16\\CORE_RL_wand_.DLL"

# Load-hooks
function init_deps()
	ENV["MAGICK_CONFIGURE_PATH"]	= "C:\\Program Files\\ImageMagick-6.9.3-Q16"
	ENV["MAGICK_CODER_MODULE_PATH"]	= "C:\\Program Files\\ImageMagick-6.9.3-Q16"
ccall((:MagickWandGenesis,libwand), Void, ())
end
init_deps()
```

### Float32sc
* Message: 'ERROR: LoadError: UndefVarError: float32sc not defined'
* Solution: Change 'temp = float32sc(img)' to 'temp = convert(Image{Gray}, img)'.

_I still need to check to be sure result has the same format. But hard since I cant get the result from 'float32sc(img)'..._

### String instead of Symbol
* Message: 'ERROR: LoadError: MethodError: `getindex` has no method matching getindex(::DataFrames.DataFrame, ::ASCIIString)'
* Solution: Change 'nameFile["nameColumn"]' to 'nameFile[:nameColumn]'