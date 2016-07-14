---
layout: post
title: 'Gophercon 2016 Recap'
---

Gophercon exists to get as many Golang developers together in one place as possible.
It's a four day event, starting with tutorials, two days of talks, and closing out
with a hackday. Due to my schedule and preferences I decided only to attend days two
and three of talks.

Thanks to [Twitch][twitch-link] the conference was available as a live stream. You will be able to
[watch all the talks][link-to-talks]. (Links to talks will be updated as they come out.)

Since the [talks][link-to-talks] are available online. I plan to give my thoughts and take
aways from each talk. That means the post will not contain a summary of the talks but
my understanding of what I took away from the talk.

## Nil talk

[Slides][nil-slides]

The gist: avoid `func NewMyStruct` and favor having custom structs work with as a `nil`. This means
the pointer receiver method (or plain receivers) should work if attributes of the struct are
in their default state. For example look at this `Line` struct:

```go
// For simplicity we'll use only ints and not show the
// calculation for slope.
type Point struct {
    x int
    y int
}

type Line struct {
    points []Point
}

func (l Line) Slope() int {
    if l.points == nil {
        return 0
    }

    // return calculated slope of points
}
```

Having the receiver methods handle `nil` attributes makes error handling a lot easier. The
same code depending on a `NewLine` constructor would have to check for errors because it
would assume the points were already added to the line.  This is a trivial example but
shows how using default values and avoiding `NewMyStruct` methods can help with implementation
and may be more idiomatic go.

Another good idea I like was using `nil` for default map values. The big caveat being to focus
only doing `nil` map passes when the map would be configuration. This allows for easy defaults
in library method calls.

Another interesting idea for `nil` is to use it as a "closer" for a channel. Since `nil` is
the default value of a channel a `select` will ignore the channel if you set it to `nil`.
Just make sure the channel has been cosed first.

## Vendoring

-- link coming soon

The resolution order for packages is now what I'd want with Go 1.5 and above.
This means that your code will look in the most specific location for a package.
It also allows for different versions of a package in the same project -- assuming
a library is vendoring it inside itself.

The lookup order is now:

1. Vendor folder
2. Package Level
3. $GOROOT
4. $GOPATH

With that resolution order in place it made me think of a potentially crazy idea.
What if we overrode the default `log` so that we could have real logs. For example
logs that were debug level, info level, etc. that could then be turned off by config.
I've not tried it but you could setup a project like this and give it a whirl.

```
myproject/
    log/
        log.go // This would wrap the normal logger and allow info/debug etc.
    myproject.go
    vendor/
        stuff*
```

Then in the code it'd look normal:

```go
package "myproject"

import "log"

func main() {
    log.Println("INFO -- Service is starting up!")
}

```

The other advantage here is that the logs could also get automatically sent to one
central location from the "wrapped" `log`. I think it'd be a nifty feature if we
could get it working without breaking the standard library. It may also give a way for
third part libraries to finally have a "standard" way to do logging.

Finally, as it relates to vendoring, the `$GOPATH` could be set to _only_ the
current project to ensure nothing extra is grabbed when doing a build.
I'm not sure if it's needed or desired, but as long as all the dependencies
are in `vendor/` then the build should be safe and no extra libs would end
up being used during compilation.

## Concurrency

[Slides][concurrency-slides]

Until the repository goes live I recommend looking at the slides for this talk.
The coolest parts were seeing how the various different ways to do concurrent
go routines works out. Having a visual of the algorithm helps it make a lot more
sense. It also lets you know if you are wasting CPU time by having go routines
that are waiting and not executing.

Downside for now is the requirement of a patched go version to get the visualizations.

One of the interesting ones can be found here: http://divan.github.io/talks/2016/gophercon/#/19

## Reflection

This talk gave me no reason to use reflection for any purpose.
I disagree with the premise that it makes code readable and adds integrity to code.

This talk lead me to always avoid reflection.  I will always try type assertion first. If I need
something more dynamic I may then go to reflection.

For example a valid use case, that I was able to derive, is if you make some kind of generic
parser of objects. That parser of objects may produce something from your objects. However,
I'd still favor using an interface and avoid using reflection in this case.

I've still not seen a real reason to use reflection that isn't solve by an interface or type
assertion.

## Creating 3rd Party Libraries

[Slides][3rd-party-slides]

Here are the basic recommendations:

* Favor using package name in library usage e.g. `http.Client` instead of `reNamedHttp.Client`
* Avoid constructor functions, try to allow `nil` structs to be used (see [nil](#nil-talk) above)
* Avoid adding logs if you can help, if you have them allow overrides and shutting them off
* Avoid returning errors if you can
* For debugging add a `Stats` and `Logging` handlers so it's easier to see what's going on
* Avoid having channels get passed in or out from the library, leave that to the consumer to manage the channel


[link-to-talks]: https://gophercon.com
[twitch-link]: https://www.twitch.tv/

[vendoring-link]: https://gophercon.com

[nil-slides]: https://speakerdeck.com/campoy/understanding-nil
[concurrency-slides]: http://divan.github.io/talks/2016/gophercon/#/
[3rd-party-slides]: http://go-talks.appspot.com/github.com/cep21/go-talks/practical-advice-for-go-library-authors.slide#1
