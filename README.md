# CRANextra
fixing the CRANextra warnings when installing packages


If you're here you must have hit by this:

Warning: unable to access index for repository http://www.stats.ox.ac.uk/pub/RWin/bin/windows/contrib/4.4:
  cannot open URL 'http://www.stats.ox.ac.uk/pub/RWin/bin/windows/contrib/4.4/PACKAGES'

Some times it's not a warning but even an error.

This is my solution, with the help of deepseek and NOT WITH ANY HELP FROM those "great developers" (#83 #91 #907 #943 etc.)

1. find your user file and profile file
   (1) `.Rprofile`: type and execute `path.expand("~")` in your R console and copy the directory path to the folder address bar, then look for `.Rprofile`
   (2) `Rprofile.site`: type and execute `R.home("etc")` in your R console and copy the directory path to the folder address bar, then look for `Rprofile.site`

2. open these two files with notepad txt

3. copy the following scripts, paste to the end of the two files

```
# fixing the CRANextra warnings when installing packages
# the following two chucks of scripts will/may run from start of R
local({
  r <- getOption("repos")  # Get the current repositories
  r <- r[names(r) != "CRANextra"]  # Remove CRANextra
  options(repos = r)  # Update the repositories
})

# the cloudyr project
# https://cloudyr.github.io/drat/
if (!require("drat")) {
    install.packages("drat")
    library("drat")
    drat::addRepo("cloudyr", "http://cloudyr.github.io/drat") # Add coudyr to repositories
}
```

4. save and close the two files

5. in the same folder of the `Rprofile.site` there should be a `repositories` file, open it and remove the line with "CRANextra", save and close

6. restart your R / R session / Rstudio / whatever


So, I'm just a nobody trying to help other newbees like me who also has little knowlege of these kind of "easy bugs".
