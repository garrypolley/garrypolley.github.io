---
layout: post
title: 'Golang: errors, routines, and channels'
---

I've been working in Golang for a few months now.  I've really started
to like the language and how similar it is to Python. Below is an example
of how I'm planning to handle errors that occur in some goroutines.

The example is borrowed from https://groups.google.com/forum/#!topic/golang-nuts/zAmaq1Q2mqA
I wanted more rationale on each part and below are the examples. I put some effort into
explaining how each part works and why it works. The comments in the code hopefully give
a better understanding as to how the go routines and channels work together. 

In order to get a full experience you'll need to update some of the code by commenting
and uncommenting parts of the code. It should be documented where that is needed.

```go
package main

import "fmt"
import "sync"
import "time"

type Error struct {
	message string
}

func (e Error) Error() string {
	return e.message
}

func main() {
	var wg sync.WaitGroup
	waitGroupLength := 8
	errChannel := make(chan error, 1)

	// Setup waitgroup to match the number of go routines we'll launch off
	wg.Add(waitGroupLength)
	finished := make(chan bool, 1) // this along with wg.Wait() are why the error handling works and doesn't deadlock

	for i := 0; i < waitGroupLength; i++ {

		go func(i int) {
			fmt.Printf("Go routine %d executed\n", i+1)

			// Sleep for the time needed for each other go routine to complete.
			// This helps show that the program exists with the last go routine to fail.
			// comment this line if you want to see it fail fast
			time.Sleep(time.Duration(waitGroupLength - i))

			time.Sleep(0) // only here so the time import is needed

			// comment out the following 3 lines to see what happens without an error
			// Note, the channel has a length of one so the last go routine to error
			// will always be the last error.

			if i%4 == 1 {
				errChannel <- Error{fmt.Sprintf("Errored on routine %d", i+1)}
			}

			// Mark the wait group as Done so it does not hang
			wg.Done()
		}(i)
	}

	// Put the wait group in a go routine.
	// By putting the wait group in the go routine we ensure either all pass
	// and we close the "finished" channel or we wait forever for the wait group
	// to finish.
	//
	// Waiting forever is okay because of the blocking select below.
	go func() {
		wg.Wait()
		close(finished)
	}()

	// This select will block until one of the two channels returns a value.
	// This means on the first failure in the go routines above the errChannel will release a
	// value first. Because there is a "return" statement in the err check this function will
	// exit when an error occurs.
	//
	// Due to the blocking on wg.Wait() the finished channel will not get a value unless all
	// the go routines before were successful because not all the wg.Done() calls would have
	// happened.
	select {
	case <-finished:
	case err := <-errChannel:
		if err != nil {
			fmt.Println("error ", err)
			return
		}
	}

	fmt.Println("Successfully executed all go routines")
}

```
[Run it on go playground](http://play.golang.org/p/N6BVTrE2_S) or see below.

<iframe src="http://play.golang.org/p/N6BVTrE2_S" frameborder="0" style="width: 100%; height: 400px"><a href="http://play.golang.org/p/N6BVTrE2_S">see this code in play.golang.org</a></iframe>

