# Assemble Bug Test

Filenames that conflict variables within `Gruntfile.js` will cause task issues.

In this example, there is a partial called `connect.hbs` which will interfere with the connect object in `Gruntfile.js`. Running assemble as part of a larger task such as `grunt serve` will error with: `Verifying property connect.livereload exists in config...ERROR` when the task hits `connect:livereload` or potentially any task accessing variables in `Gruntfile.js` after the `assemble` task. Simply running `grunt assemble` will be fine. You can successfully work your way to running the `grunt serve` task by running `grunt assemble` manually first, and then commenting out the `clean:server` and `assemble` tasks to serve the manually assembled code in temp.

You won't notice the issue straight away if a task such as `grunt serve` is already running, but the next time you go to start the server or build you will be baffled as to why something that was just working suddenly errors. Rename the file and the project will run again.

## Steps to reproduce
1.  Clone this repository `git clone https://github.com/davechiu/assemble-io-naming-bug-test.git`
2.  Run `npm install`
3.  Run `bower install`
4.  Run `grunt serve`
5.  Rename `app/templates/partials/!connect.hbs` to `app/templates/partials/connect.hbs`
6.  See that everything is still running
7.  Stop the server `^C`
8.  Restart the server `grunt serve`
9.  Error.

## Suggestion
Perhaps throw a warning about name conflicts?