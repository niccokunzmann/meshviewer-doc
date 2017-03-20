# Debug

## Find errors with sentry

We provide a branch with sentry [https://sentry.io/](https://sentry.io/) and it will send errors reports to your or our sentry server. This will improve quality and we depend less on user reports \(not every user reports or we don't get the error forwarded\).

### Advantages

* Find errors from users with different usage of meshviewer.
* Reports include a full stacktrace, browser version and other information.

You can use the Saas version or host it yourself. Or ask us for an instance, we are happy for more feedback from different instances.

You might need to rebase the debug branch to have your settings.

## Find errors without sentry

### Browsersync

We use Browsersync for local development and `grunt serve` will show a second port with Browsersync settings and tools. It includes winere, a remote inspection tool and allows to sync tabs. The web-interface can often be found under port 3001.

### Javascript console

Use console.log, it only throws a warning and no error in linter.

