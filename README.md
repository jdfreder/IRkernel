# Native R kernel for IPython

This is still experimental and unreliable. Your code should be safe,
since IPython handles saving and loading notebooks in another process, but
you'll lose all your variables if it crashes.

##Installing

You'll need zmq development headers to compile rzmq, as well curl headers for
R devtools. On a recent Ubuntu/Debian installation, you can get these
with:

```Shell
sudo apt-get install libzmq3-dev libcurl4-openssl-dev
```

or with homebrew:

```Shell
brew install zmq
# or upgrade
brew update
brew upgrade zmq
```

If using MacPorts on OS X, make sure an [X server is intalled](http://xquartz.macosforge.org/), open a terminal and do the following:

 * `sudo port install zmq`
 * Direct the compiler to use MacPorts libraries using

        export CPATH=/opt/local/include
        export LIBRARY_PATH=/opt/local/lib
 * Start `R` in the same terminal, and proceed as below:

We need development versions of several packages from Github for now, due to
recent fixes. First, you need to make sure you have the `devtools` R package
available. If you don't, at the R console type:

```coffee
install.packages("devtools")
```

Then, you can install the necessary development dependencies with:

```coffee
library(devtools)
install_github('jeroenooms/jsonlite')
install_github('armstrtw/rzmq', pull=8, ref=NULL)
install_github("takluyver/IRdisplay")
install_github("takluyver/IRkernel")

# Only if you have IPython 3 or above installed:
IRkernel::installspec()
```

You'll also need [IPython](http://ipython.org/). If you already have a Python
environment set up, install IPython using your preferred tools. If not,
installing [Anaconda](http://continuum.io/downloads) is the quickest way to get
everything you need.

# Running the notebook

If you have IPython 3 installed, you can create a notebook and switch to
IRkernel from the dropdown menu. In IPython 2.x, you will need to start the
notebook with this command:

```Shell
ipython notebook --KernelManager.kernel_cmd="['R', '-e', 'IRkernel::main()', '--args', '{connection_file}']"
```

You can also substitute 'qtconsole' or 'console' for 'notebook' in this command.
