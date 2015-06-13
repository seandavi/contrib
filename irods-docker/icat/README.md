```
pull seandavi/irods_icat:4.0.3
docker create -v /var/lib/postgresql/9.3/main --name irodsDb seandavi/irods_icat:4.0.3 /bin/true
docker run -p 1247:1247 -v /data/Vault:/var/lib/irods/Vault -v /data/CCRBioinfo:/data/CCRBioinfo --volumes-from=irodsDb -d -t seandavi/irods_icat:4.0.3 'PASSWORD'
```
