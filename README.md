Project 0: Introduction to Go concurrency and testing
==

## Setting up Go

You can download and install Go for your operating system from [the official site](https://golang.org/doc/install).

**Please make sure you intall Go version 1.17. The Gradescope autograder uses Go version 1.17 too.**

### Using Go on AFS

For those students who wish to write their Go code on AFS (either in a cluster or remotely), follow
the guidance to download Go for linux [here](https://golang.org/doc/install). However, instead of 
extracting the archive into `/usr/local` as mentioned in the installation instructions, extract the 
archive into a custom location in your home folder with following commands:

```bash
$ tar -C $HOME/(custom_directory) -xzf go1.17.linux-amd64.tar.gz
```

Then, instead of adding `/usr/local/go/bin` to the PATH environment variable as mentioned in the
installation instructions, replace `/usr/local` with the path in which you have extracted the archive 
in the step before:

```bash
$ export PATH=$HOME/(custom_directory)/go/bin:$PATH
```

You will also need to set the `GOROOT` environment variable to be the path which you have just extracted
the archive (this is required because Go is installed in a custom location on AFS machines):

```bash
$ export GOROOT=$HOME/(custom_directory)/go
```

## Part A: Implementing a key-value messaging system

This repository contains the starter code that you will use as the basis of your key-value messaging system
implementation. It also contains the tests that we will use to test your implementation,
and an example 'server runner' binary that you might find useful for your own testing purposes.

If at any point you have any trouble with building, installing, or testing your code, the article
titled [How to Write Go Code (with GOPATH)](https://golang.org/doc/gopath_code.html) is a great resource for understanding
how Go workspaces are built and organized. You might also find the documentation for the
[`go` command](http://golang.org/cmd/go/) to be helpful. As always, feel free to post your questions
on Piazza as well.

### Running the official tests

To test your submission, we will execute the following command from inside the
`src/github.com/cmu440/p0partA` directory:

```sh
$ go test
```

We will also check your code for race conditions using Go's race detector by executing
the following command:

```sh
$ go test -race
```

To execute a single unit test, you can use the `-test.run` flag and specify a regular expression
identifying the name of the test to run. For example,

```sh
$ go test -race -test.run TestBasic1
```

### Fix the missing module errors when running `go test`

To fix the missing module errors in Go 1.17, you can generate a module file as following:

In directory `src/github.com/cmu440`, execute the following command:

```sh
$ go mod init github.com/cmu440
```

This will auto-generate a go.mod file in the directory. As long as you include that file in the repo, the project will work fine. (e.g. `go test` inside `src/github.com/cmu440/p0partA` or `src/github.com/cmu440/p0partB`)

### Testing your implementation using `srunner`

To make testing your server a bit easier (especially during the early stages of your implementation
when your server is largely incomplete), we have given you a simple `srunner` (server runner)
program that you can use to create and start an instance of your `KeyValueServer`. The program
simply creates an instance of your server, starts it on a default port, and blocks forever,
running your server in the background.

To compile and build the `srunner` program into a binary that you can run, execute the three
commands below (these directions assume you have cloned this repo to `$HOME/p0`):

```bash
$ export GOPATH=$HOME/p0
$ go install github.com/cmu440/srunner
$ $GOPATH/bin/srunner
```

The `srunner` program won't be of much use to you without any clients. It might be a good exercise
to implement your own `crunner` (client runner) program that you can use to connect with and send
messages to your server. We have provided you with an unimplemented `crunner` program that you may
use for this purpose if you wish. Whether or not you decide to implement a `crunner` program will not
affect your grade for this project.

You could also test your server using Netcat as you saw shortly in lecture (i.e. run the `srunner`
binary in the background, execute `nc localhost 9999`, type the message you wish to send, and then
click enter).

## Part B: Testing a squarer

Once you have written your test, simply run

```sh
$ go test
```

in `p0partB` to confirm that the test passes on the correct implementation.

## Submission

Submit a zip file created by running `make handin` from `src/github.com/cmu440`. **Do not change the names of the files (`server_impl.go` and `squarer_test.go`) as this will cause the tests to fail.**
