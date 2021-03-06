# 2.0.1

FIXED race condition that causes write after end errors


# 2.0.0

REMOVED deprecated methods.

FIXED bug in purgeQueues.


# 1.2.4

Updated to Babel.js 4.7.1.


# 1.2.3

Updated to Babel.js 4.4.5.


# 1.2.2

FIXED trying to catch "write after" end errors.


# 1.2.1

Upgraded to 6to5 3.0.


# 1.2.0

ADDED support for queuing with streams.

For example, to queue all the jobs from the source stream, and log the queued
job IDs:

  source
    .pipe( queue.stream() )
    .pipe( process.stdout );

ADDED `queueJob` as alias for `pushJob` and `Ironium.queueJob` shortcut.

ADDED you can use queueJob, delayJob, etc without an object reference.

CHANGED switched from Traceur to 6to5, which works much better for 3rd party
libraries.


# 1.1.0

ADDED you can now use pushJob with a string or buffer; objects are always
serialized to JSON.

CHANGED push deprecated, use pushJob instead

CHANGED delay deprecated, use delayJob

CHANGED each deprecated, used eachJob instead

CHANGED schedule deprecated, use scheduleJob instead

CHANGED once deprecated, use runOnce instead

CHANGED reset deprecated, use purgeQueues instead

CHANGED width deprecated, use queueWidth instead


# 1.0.3

FIXED no longer user timeout to detect connection failure, this allows better
concurrency for job push on slow connections.


# 1.0.1

REMOVED "possible EventEmitter memory leak detected" message when we have
hundred of writers pushing to the same queue.


# 1.0.0

ADDED emit `error` events and output error message when `DEBUG=ironium`


# 0.13.0

ADDED when executing job, current job ID available from process.domain.jobID

Since the domain is accessible in callbacks and event handlers, you can use this
to trace the execution of the job, specifically for logging messages.


# 0.12.1

FIXED make sure to unref all timeout/interval.


# 0.12.0

ADDED Ironium will output to console if run with `DEBUG=ironium` or `DEBUG=*`.

ADDED The methods start, stop, once and reset are now bound to an instance of
Ironium, so can be passed directly to Mocha before/after methods.

REMOVED No longer emitting `error` events.


# 0.11.9

CHANGED zero timeouts and delay when running in development or test environments


# 0.11.8

FIXED stupid bug when fetching queued jobs


# 0.11.7

CHANGED just in case defensive programming at practice


# 0.11.6

Trying better handling when establishing connection


# 0.11.5

FIXED was testing error instead of message, incorrect in some envs


# 0.11.4

FIXED queue processing may stop for some rejected promises


# 0.11.3

FIXED properly detect error message


# 0.11.2

CHANGED ignore DRAINING error


# 0.11.1

CHANGED ignore connection closed error when processing queue


# 0.11.0

ADDED queue.delay works just like queue.push but delays processing of the job.

```
queue.delay(job, duration, callback?)
```

Duration is either a number or a string.  The default unit is milliseconds, but
you can specify a string with units, such as "5m" or "3 hours".

Valid units are `ms`, `seconds`, `minutes`, `hours`, `days` and `years`.  You
can write each unit as plural ("1 hours"), singular ("1 hour") or first letter
only ("1h").


# 0.10.3

FIXED generate error when one not available


# 0.10.2

FIXED error handling for sessions and reset


# 0.10.0

Because ES7, Ironium's API changed to return promises instead of thunks.

If you're using Traceur, and you wanted to duplicate a job in queue0 to queue1
and queue2, you could do this:

```
queue0.each(async function(job) {
  await queue1.push(job);
  await queue2.push(job);
});
```


# 0.9.15

Upgraded to Traceur 0.0.18.


# 0.9.14

FIXED: don't block $schedule queue waiting for jobs to run.


# 0.9.13

CHANGED: workers.once() fails if any scheduled job fails.

FIXED: if request to queue scheduled job fails, try again.


# 0.9.12

FIXED: scheduled jobs not processed until next schedule.


# 0.9.11

FIXED: don't care for close errors while reserving jobs.


# 0.9.10

FIXED: more informative close/error messages.


# 0.9.9

Upgraded to Traceur 0.0.10. 


# 0.9.8

FIXED: should not warn about closed connection, unless it interrupts request.

CHANGED: schedule time should be ISO string.


# 0.9.7

CHANGED: session ID now indicates if it's put session or worker number.

FIXED: error handling for connection close/error without using timeout.

FIXED: trying to work around Iron.io disconnect issue.


# 0.9.6

CHANGED: documentation uses `ironium` instead of `workers`.

FIXED: connection errors not reported correctly.


# 0.9.5

FIXED: bug when cleaning out Beanstalkd queue.


# 0.9.4

CHANGED: use of queues on their own will not prevent process from completing.


# 0.9.3

FIXED: scheduled jobs not running in production.


# 0.9.2

FIXED: hostname/port not picked up from configuration.


# 0.9.1

Configuration gets separate section for setting up Iron.io server.


# 0.9.0

Scheduler now queues job for execution, this will allow using a scheduler
service.

Scheduler now accepts scheduled time as either Date, interval (number or
string), or an object with start time, end time and interval.


# 0.8.0

Methods like `once`, `reset` and `push` now return thunks instead of promises.
Disappointing for some, but easier for those of us using
[Mocha](http://visionmedia.github.io/mocha/) and
[co](https://github.com/visionmedia/co).


# 0.7.3

Testing with [Travis-CI](https://travis-ci.org/assaf/ironium).


# 0.7.2

Fixed: need Error object when reporting connection closed


# 0.7.1

Use [monolithed/ECMAScript-6](https://github.com/monolithed/ECMAScript-6) to
implement promises.


# 0.7.0

Removed `workers.fulfill`, please use
[thunks](https://github.com/visionmedia/co#thunks-vs-promises) instead.

Minor performance improvement.


# 0.6.0

Removed `workers.push` and `workers.each`, referencing queues is better for
testing.

Renamed count to width (number of workers used in parallel).

Tests!


# 0.5.3

Allow multiple queue handlers.

Added `workers.push`, `workers.each` and `workers.webhookURL` convenience
methods.


# 0.5.2

Using [co](https://github.com/visionmedia/co).


# 0.5.1

Added `workers.fulfill` to ease using generators with callbacks.

Added documentation for logging.


# 0.5.0

Preliminary support for generators.


# 0.4.0

Use native Promise instead of Q.
