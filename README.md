# JenkinsTest

## Run

```bash
cp .env.template .env
# modify env variables in `.env` file

docker compose up -d && docker compose logs -f --tail=1000

docker exec ${CONTAINER_ID or CONTAINER_NAME} cat /var/jenkins_home/secrets/initialAdminPassword
```

## References

- <https://github.com/jenkinsci/docker>
- <https://hudi.blog/install-jenkins-with-docker-on-ec2/>
