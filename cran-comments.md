This version addresses the failure to build for r-release-osx-x86_64-mavericks
by testing for an earlier version of R, 3.1.3.

## Test environments
* local Windows 8.1 64-bit, R 3.2.2
* local Windows 8.1 64-bit, R 3.1.3
* win-builder (devel and release)

## R CMD check results
There were no ERRORs or WARNINGs.

There were 2 NOTEs:
* checking CRAN incoming feasibility ... NOTE
Maintainer: 'Steve Myles <steve@mylesandmyles.info>'
New submission

License components with restrictions and base license permitting such:
  MIT + file LICENSE
File 'LICENSE':
  YEAR: 2015
  COPYRIGHT HOLDER: Steve Myles

* checking top-level files ... NOTE
File README.md cannot be checked without 'pandoc' being installed.

## Downstream dependencies
N/A
