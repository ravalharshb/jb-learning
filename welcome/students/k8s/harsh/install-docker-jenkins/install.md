<h1>JENKINS INSTALLATION REPOSITORY</h1>

<h2> READY </h2>
```bash
git clone --branch jenkins-latest  https://github.com/yanivomc/docker-cicd.git
cd docker-cicd
```

<h2> SET </h2>
```bash
docker compose -f docker-compose-jenkins.yml  up -d
```

<h2> GO </h2>
After ~2 minutes you can browse your remote ip:
```bash
Browse: http://[REMOTEIP]:8080/
```
1. User:pass - admin:admin

*Not required for one node:* 
To scale our slave nodes run: 
```bash
docker compose -f docker-compose-jenkins.yml  up -d  --scale jenkins-slave=2
```

<h2> DONE. COMPLETED. FINITO </h2>
