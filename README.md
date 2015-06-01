# docker-ruby-phantomjs

This docker image is intended to run Cucumber with PhantomJS, but not limited to. It is mainly based on the offical Ruby image. PhantomJS is the only dependency added to it.

The image itself has no opinion on where you should put your source code, since you may not use it with any source code. But if you do want to mount your source code, you can run similar command as follow to create the volume and working directory:
```
docker run -it --rm -w /usr/src/app -v "$(pwd)":/usr/src/app killercentury/ruby-phantomjs bash
```