# Debug

## Find errors with sentry
We provide a brnach with sentry https://sentry.io/ and it will send errors reports to your or our sentry server. This will improve quality and we depent less on user reports (notr every user reports or we don't get the error forwarded).

### Advantages
- Find errors from users with different useage of meshviewer.
- Reports include a full stacktrace, browser version and other informations.

You can use the Saas version or host it yourself. Or ask us for an instance, we are happy for more feedback from different instances.

You might need to rebase the debug branch to have your settings.

## Find errors without sentry

### Browsersync
We use browsersync for local development and `grunt serve` will show a second port with Browsersync settings and tools. It includes wineew, a remote incpection tool and allows to sync tabs. The webinterface can often be found under port 3001.

### Javascript console
Use console.log, it only throws a warning and no error in linter.