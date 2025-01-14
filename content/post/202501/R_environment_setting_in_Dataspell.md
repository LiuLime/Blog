---
title: RWrapper terminated Error when Setting R Interpreter in DataSpell
description: "RWrapper terminated, exitcode: 134 error caused by incompatible package architecture with M1 core."
date: 2025-01-14T11:18:44+09:00
image: /Rwrapper_terminated_error.png
categories:
    - Programming
    - Environment
tags:
    - Error
# You can add weight to some posts to override the default sorting (date descending)
weight: 2
---

## Background
PC: MacOS M1 core       
Software: JetBrains DataSpell v.2023        
Interpreter Environment: 
- python 3.12 in conda virtual environment
- R 4.11 in `/usr/local/bin/R` # downloaded by homebrew
```bash
# check R path
which R

# >>> /usr/local/bin/R
```

## Error
When setting R Interpreter in JetBrains DataSpell v.2023 on MacOS M1 core, 
error `RWrapper terminated, exitcode: 134`  occuered.



```bash
# Example usr_name=luckydog
Cannot run console
RWrapper terminated, exitcode: 134

rpath: RPaths(home=/Users/luckydog/miniconda3/envs/datapreprocess/lib/R,
share=/Users/luckydog/miniconda3/envs/datapreprocess/lib/R/share,
include=/Users/luckydog/miniconda3/envs/datapreprocess/lib/R/include,
doc=/Users/luckydog/miniconda3/envs/datapreprocess/lib/R/doc,
path=/Users/luckydog/miniconda3/bin:/Users/luckydog/miniconda3/condabin:/opt/homebrew/bin:/opt/homebrew/sbin:/opt/local/bin:/opt/local/sbin:/usr/local/bin:/System/Cryptexes/App/usr/bin:/usr/bin:/bin:/usr/sbin:/sbin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/local/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/appleinternal/bin:/Library/Apple/usr/bin:/Library/TeX/texbin:/Users/luckydog/.cargo/bin, ldPath=/Users/luckydog/miniconda3/envs/datapreprocess/lib/R/lib:/Users/luckydog/miniconda3/envs/datapreprocess/lib:/Users/runner/miniforge3/conda-bld/r-base-split_1734433510517/_build_env/lib/jvm/lib/server)  
stdout: stderr: /Applications/DataSpell.app/Contents/plugins/r-plugin/rwrapper-arm64-osx --with-timeout --crash-report-file /private/var/folders/qy/2mqk95_j71zdsf092yg78fsc0000gn/T/rwrapper-crash-report1736748538955.txt
dyld[43972]: Library not loaded: @library_path/libR.dylib Referenced from: 20FB2B40-38F5-3A10-8EBA-570B873BD1AE> /Applications/DataSpell.app/Contents/plugins/r-plugin/rwrapper-arm64-osx
Reason: tried: "/Users/luckydog/miniconda3/envs/datapreprocess/lib/R/lib/libR.dylib" (mach-o file, but is an incompatible architecture (have "x86_64", need "arm64e" or "arm64")), "/Users/luckydog/miniconda3/envs/datapreprocess/lib/libR.dylib" (no such file), "/Users/runner/miniforge3/conda-bld/r-base-split_1734433510517/_build_env/lib/jvm/lib/server/libR.dylib" (no such file), "/usr/lib/libR.dylib" (no such file, not in dyld cache)

```
I noticed the sentence 'mach-o file, but is an incompatible architecture (have "x86_64", need "arm64e" or "arm64")' in error report,
so I guess the architecture of packages are incompatible with my M1 PC.

## Verification
### 1. verify conda architecture platform is intel or arm64
```bash
conda info

# >>> platform :osx-64  # intel
```
### 2. verify R architecture
- (optional) set to launch R in terminal
```bash
vim ~/.zshrc
```
add 'export PATH="/Library/Frameworks/R.framework/Resources/bin:$PATH"' in .zshrc file to add R execute path in global environment path and can launch R in terminal. 

- check R info
```bash
R --version

# >>> platform intel
```

## Solution
### 1. Convert conda config from intel to arm architecture
```bash
conda config --set subdir osx-arm64
```
Then create new conda environment.

### 2. two ways to change R architecture, 
one way is to change R architecture in base environment and set R interpreter path as `/usr/local/bin/R`, 
one way is to download R through conda-forge in conda virtual environment and set R interpreter path as `/Users/[usr_name]/miniconda3/envs/[env_name]/bin/R`.
#### (1). download R arm architecture
[R arm version download link](https://cran.r-project.org/bin/macosx/), install and check R version in base environment again.

#### (2). install R through miniconda3/miniforge3
Insure miniconda3 changed the config in step 1;
miniforge3 install arm64 architecture in default.
```bash
conda install -c conda-forge r-base r-essenrials
```

### 3. Setting R interpreter in Dataspell
Interpreter settings-> R settings-> Project R Interpreter-> '/usr/local/bin/R' or '/Users/[usr_name]/miniconda3/envs/[env_name]/bin/R'

Figure1. R interpreter setting API      
![R interpreter setting](/R_interpreter_setting.png)


**Supplement:     
I installed miniforge3 instead of miniconda3 before install R in virtual environment, so the path in figure 1 showed miniforge3 instead of miniconda3**

@LiuLime
copyright all reserved