# install R (on Linux)

## website

link: https://cran.r-project.org/

## repository update

Ubuntu instructions.

```
# update indices
apt update -qq
# install two helper packages we need
apt install --no-install-recommends software-properties-common dirmngr
# import the signing key (by Michael Rutter) for these repo
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
# add the R 4.0 repo from CRAN -- adjust 'focal' to 'groovy' or 'bionic' as needed
add-apt-repository "'deb https://cloud.r-project.org/bin/linux/ubuntu '$(lsb_release -sc)'-cran40/'"
```

In my case, the `add-apt-repository` resolved to: 

```
deb https://cloud.r-project.org/bin/linux/ubuntu 'focal'-cran40/
```
and this is invalid (apparently).

So, fix this:

```
root@cplusdev:/home/steve/Desktop# add-apt-repository deb https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/
Error: need a single repository as argument
root@cplusdev:/home/steve/Desktop# add-apt-repository "deb https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/"
Hit:1 http://ca.archive.ubuntu.com/ubuntu focal InRelease
Get:2 http://security.ubuntu.com/ubuntu focal-security InRelease [109 kB]
Get:3 http://ca.archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]
Get:4 http://ca.archive.ubuntu.com/ubuntu focal-backports InRelease [101 kB]                            
Get:5 https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/ InRelease [3,622 B]                                
Get:6 https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/ Packages [31.6 kB]
Fetched 359 kB in 2s (234 kB/s)
Reading package lists... Done
root@cplusdev:/home/steve/Desktop#
```

Finally, install with:

```
apt install --no-install-recommends r-base
```

## studio

```
pre-request

link: https://linuxconfig.org/how-to-install-rstudio-on-ubuntu-20-04-focal-fossa-linux

sudo apt update
sudo apt -y install r-base gdebi-core

wget https://download1.rstudio.org/desktop/bionic/amd64/rstudio-1.4.1106-amd64.deb

sudo gdebi rstudio-1.4.1106-amd64.deb

and run

rstudio

I suggest going Tools->Global Options->Appearance and picking some other colors/font sizes. 

```

## test installation

Inside r studio:

```

R version 4.0.4 (2021-02-15) -- "Lost Library Book"
Copyright (C) 2021 The R Foundation for Statistical Computing
Platform: x86_64-pc-linux-gnu (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under certain conditions.
Type 'license()' or 'licence()' for distribution details.

  Natural language support but running in an English locale

R is a collaborative project with many contributors.
Type 'contributors()' for more information and
'citation()' on how to cite R or R packages in publications.

Type 'demo()' for some demos, 'help()' for on-line help, or
'help.start()' for an HTML browser interface to help.
Type 'q()' to quit R.

> print("hello world")
[1] "hello world"
> 

```

## test from command line

```
steve@cplusdev:~/projects/installR$ R

R version 4.0.4 (2021-02-15) -- "Lost Library Book"
Copyright (C) 2021 The R Foundation for Statistical Computing
Platform: x86_64-pc-linux-gnu (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under certain conditions.
Type 'license()' or 'licence()' for distribution details.

  Natural language support but running in an English locale

R is a collaborative project with many contributors.
Type 'contributors()' for more information and
'citation()' on how to cite R or R packages in publications.

Type 'demo()' for some demos, 'help()' for on-line help, or
'help.start()' for an HTML browser interface to help.
Type 'q()' to quit R.

> print("hello world")
[1] "hello world"
> q()
Save workspace image? [y/n/c]: n
```

## test as a script

```
steve@cplusdev:~/projects/installR$ cat hello.R
#!/usr/bin/env Rscript
sayHello <- function(){
   print('hello')
}

sayHello()

steve@cplusdev:~/projects/installR$ Rscript hello.R
[1] "hello"

```

or (since we used the bin thing)

```
steve@cplusdev:~/projects/installR$ chmod +x hello.R
steve@cplusdev:~/projects/installR$ ./hello.R 
[1] "hello"
```


