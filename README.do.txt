!bquote
`gbox-glog` is a gbox that performas generalized log transform on a set of standard genes. 
!equote

===== Prerequisites =====

You mainly need a working copy of "Docker": "http://docker.com". It is used
exclusively to manage system configurations for running numerous tools
across numerous platforms.

===== Installation =====

* All docker images are at "https://hub.docker.com/u/granatumx".
* All github repos are at "https://github.com/granatumx/*".

First set up your scripts and aliases to make things easier. This command should pull the container if
it does not exist locally which facilitates installing on a server.
!bc sys
source <( docker run --rm -it granatumx/scripts:1.0.0 gx.sh )
!ec

This command makes `gx` available. You can simply run `gx` to obtain a list of scripts available.

The GranatumX database should be running to install gboxes. The gbox sources do not need to be installed.
A gbox has a gbox.tgz compressed tar file in the root directory which the installer copies out and uses
to deposit the preferences on the database. Since these gboxes are in fact docker images, they will be
pulled if they do not exist locally on the system. Convenience scripts are provided for installing specific gboxes.

!bc sys
$ gx run.sh                                  # Will start the database, taskrunner, and webapp
$ gx installGbox.sh granatumx/gbox-py:1.0.0  # Install this gbox

# Now go to http://localhost:34567 and see this gbox installed when you add a step.
!ec

===== Notes =====

Glog transformation takes the form:

**        $y = log((x + sqrt(x^2 + c))/2)$

In our implementation, `c` is calculated based on a selected housekeeping gene and a selected background gene. These
two genes are selected as the gene whose expression levels have the least standard deviation across all samples,
amongst most `n` highly/lowly expressed genes.
