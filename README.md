A Docker container that runs the A-plus
Learning Management System exposed to port 8000.

Note that the A-plus front service alone does not provide
capability to implement or host learning material or exercises.
The front connects to different material or assessment services
that provide interactive content to learners. A common
counterpart for content services is the
[A-plus MOOC-grader](https://hub.docker.com/r/apluslms/run-mooc-grader/).

See into the [A-plus template course](https://github.com/apluslms/course-templates)
that includes a Docker compose configuration to develop and test course content.

### Usage

A-plus is installed in `/srv/aplus`.
You can mount development version of the A+ source code on top of that, if you wish.

Location `/data` is a volume and contains submission files, database and secret key.
It is world writable, so you can run this container as normal user.

Partial example of `docker-compose.yml` (volumes are optional of course):

```yaml
services:
  plus:
    image: apluslms/run-aplus-front
    volumes:
    # named persistent volume (until removed)
    # - data:/data
    # mount development version
    # - /home/user/a-plus/:/srv/aplus/:ro
    ports:
      - "8000:8000"
    depends_on:
      - grader
volumes:
  data:
```
