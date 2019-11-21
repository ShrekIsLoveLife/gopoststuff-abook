End of Support
--------------
I am no longer planning on updating or maintaining this.
I have moved to nyuu.
There is lack of support or compatibility in some VPS technologies that make this non-viable to keep up. I was going to write some wrappers that emulate mmap on Windows and older Kernels or certain vm and container technologies, but nyuu exists and works for my needs.


GoPostStuff-abook
===========

GoPostStuff-abook is a simple client for posting binaries to Usenet, written in Go. If you've
seen/used [newsmangler] [1], imagine that but faster.
This is an updated version of [GoPostStuff] [2].

  [1]: https://github.com/madcowfred/newsmangler/ "newsmangler"
  [2]: https://github.com/madcowfred/GoPostStuff/ "GoPostStuff"

Features
--------
* Multiple server support with multiple connections per server.
* Native TLS support so you don't need to use stunnel or equivalent frippery.
* Fast: a basic Linode VPS can push *250Mbit* of TLS-encrypted data while using 50-60%
  of a single CPU (Intel(R) Xeon(R) CPU E5-2680 v2 @ 2.80GHz).


Requirements
------------
* A working [Go installation] [2]
* A Usenet server that allows posting

  [2]: http://golang.org/doc/install  "Getting Started - The Go Programming Language"

Installation
------------
1. Initialize a directory to store Go files:

        mkdir ~/go
        export GOPATH=~/go

1.  Get and install GoPostStuff-abook - this will make a ~/go/bin/gopoststuff-abook binary:

        go get github.com/ShrekIsLoveLife/gopoststuff-abook/
        go install github.com/ShrekIsLoveLife/gopoststuff-abook/

3. Copy sample.gopoststuff.conf to ~/.gopoststuff.conf and edit the options as appropriate.

        cp ~/go/src/github.com/ShrekIsLoveLife/gopoststuff-abook/sample.gopoststuff.conf ~/.gopoststuff.conf
        vim ~/.gopoststuff.conf

4. Run gopoststuff-abook!

Usage
-----

``gopoststuff-abook [-c "CONFIG"] [-d] [-g "GROUP"] [-s "SUBJECT"] [-v] file1 file2 ... fileN``

* -c "CONFIG": Use an alternate configuration file.
* -allcpus: Use all CPUs for stuff [ALPHA]
* -cpuprofile "file": Write CPU profiling information to FILE
* -d: Use directory posting mode. Each fileN argument _must_ be a directory. All files in each
  directory will be posted using the _directory name_ as the subject.
* -g "GROUP": Post to GROUP instead of the global/DefaultGroup config option. (comma separated)
* -s "SUBJECT": Use subject posting mode. All files will be posted using SUBJECT as the subject.
  Directories supplied as arguments are always recursed into.
* -v: Verbose mode. This will spam a lot of extra debug information.
* -version: prints the current gps version.
* -nzb "test.nzb": Create nzb file after posting.
* -rarpw "PASSWORD": Add password for rar archives to nzb head.
* -server "SERVER": Use specified server to post
* -version: prints the current gopoststuff-abook version.
* -host: Hostname to use in Message-ID
* -prefix: String to place at the start of every subject line - a space will be added.
* -from: The 'From' address to put on posts.
* -from: The 'From' address to put on posts.
* -flushcon: The time in seconds between temporary disconnects from the Usenet Server to prevent timeouts. (default 5000)
* -waittime: The waiting time in seconds time before re-connect for flushcon. (default 10)


Example
-------
Let's say you have some files that you would like to post:

* Cool Files/
    + cool.rar
    + cool.r00
    + cool.r01
    + cool.sfv

You can post it with the subject "Cool Files" like so:

``gopoststuff-abook -d "Cool Files"``

or with a different subject like so:

``gopoststuff-abook -s "This is a different subject" "Cool Files"``
