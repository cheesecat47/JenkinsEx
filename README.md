# JenkinsTest

## Run

```bash
cp .env.template .env
# modify env variables in `.env` file

docker compose up -d && docker compose logs -f --tail=1000

docker exec -it -u root jenkins-jenkins-1 bash
chown jenkins:jenkins /var/run/docker.sock && chown jenkins:jenkins /usr/bin/docker-compose
```

## References

- <https://github.com/jenkinsci/docker>
- <https://hudi.blog/install-jenkins-with-docker-on-ec2/>
