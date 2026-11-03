docker exec vcs_server_local mkdir -p /tmp/https-manual

docker exec vcs_server_local openssl req -x509 -newkey rsa:2048 -noenc -sha256 -days 30 -keyout /tmp/https-manual/valid.key -out /tmp/https-manual/valid.crt -subj "/CN=localhost" -addext "subjectAltName=DNS:localhost,IP:127.0.0.1" -addext "basicConstraints=critical,CA:FALSE" -addext "extendedKeyUsage=serverAuth"

docker exec vcs_server_local openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:2048 -out /tmp/https-manual/mismatch.key

docker cp vcs_server_local:/tmp/https-manual/. .\https\

Set-Content -Path '.\empty.crt' -Value '' -NoNewline -Encoding ascii
Set-Content -Path '.\empty.key' -Value '' -NoNewline -Encoding ascii