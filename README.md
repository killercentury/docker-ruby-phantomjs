# docker-ruby-phantomjs

This docker image is intended to run Cucumber with PhantomJS, but not limited to. It is mainly based on the offical Ruby image. PhantomJS is the only dependency added to it.

The image itself has no opinion on where you should put your source code, since you may not use it with any source code. But if you do want to mount your source code, you can run similar command as follow to create the volume and working directory:
```
docker run -it --rm -w /usr/src/app -v "$(pwd)":/usr/src/app killercentury/ruby-phantomjs bash
```

## Using Bundler

### Choice 1
By default, if you simply run bundle install like this:
```
docker run -it --rm -w /usr/src/app -v "$(pwd)":/usr/src/app killercentury/ruby-phantomjs bundle install
```
Most bundle related files (configs, gems, cache, executables) will be inside the "/usr/local/bundle" folder instead of persistent in your project folder, which means you need to do a full bundle install again if you launch a new container.

### Choice 2
However, this may not be ideal for some situation that you need a fast build time. Then you can run command as follow to persist all the configs, gems, executable relative to your project base folder:
```
docker run -i --rm -v "$(pwd)":/usr/src/app -w /usr/src/app -e BUNDLE_APP_CONFIG='/usr/src/app/.bundle' killercentury/ruby-phantomjs bundle install --path vendor/bundle --binstubs
```

## Runing Executables
Take Cucumber for example, you can run it as follow if you have done bundle install as the choice 2 above.
```
docker run -i --rm -v "$(pwd)":/usr/src/app -w /usr/src/app -e BUNDLE_APP_CONFIG='/usr/src/app/.bundle' --link web:web killercentury/ruby-phantomjs bin/cucumber features/
```