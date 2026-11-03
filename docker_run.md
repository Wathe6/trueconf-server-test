docker run -d `
  --name vcs_server_local `
  --network bridge `
  -p 127.0.0.1:8080:80 `
  -p 127.0.0.1:8443:443 `
  -p 127.0.0.1:4307:4307 `
  -e ADMIN_USER=tc_admin `
  -e ADMIN_PASSWORD=password `
  --mount type=volume,source=trueconf_qa_data,target=/opt/trueconf/server/var/lib `
  trueconf/trueconf-server:stable