from alpine:3.19
run apk update && apk add socat

#-----------------------------------------------------------------------------
copy --chmod=755 <<-"eot" /opt/bin/httpok.sh
	#!/bin/sh
	while IFS=':' read key val && [ ${#key} -gt 1 ]; do : ; done
	cat <<"eof"
		HTTP/1.1 200 OK
		Content-Type: text/html; charset=UTF-8
		Content-Encoding: UTF-8
		Accept-Ranges: bytes
		Connection: close
		
		<html>
		<head>
		<title>Okay</title>
		</head>
		<body>
		Okay
		</body>
		</html>
	eof
eot

#-----------------------------------------------------------------------------
expose 8080
cmd ["/usr/bin/socat", "TCP4-LISTEN:8080,fork,reuseaddr", "exec:/opt/bin/httpok.sh"]
