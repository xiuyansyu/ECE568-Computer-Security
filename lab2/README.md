##Server: 
Create a context object followed by initializing and configuring it to hold the configuration of the server. This is done to secure an SSL. This will set the appropriate key, certificate, CA location, supported cipher suite and verification mode. We then create a TCP socket that listens for connections. Whenever a new connection is accepted, a child process is forked which handles the client requests. The child processes the SSL handshake and reports error if the client fails to provide a certificate or if the certificate is invalid. If the certificate is verified, we display the client's details and start handling the client request. If the SSL read or write is interrupted prematurely (eg: client is closed), an error message is reported. Once the client's message is received and replied to, the SSL socket is terminated by SSL_shutdown.

##Client: 
The Client initialization is similar to the server’s one. Once the appropriate key, certificate, desired cipher suite and protocol are set, a TCP connection is initiated to the server. Then it proceeds to initiate the SSL handshake followed by verification of the server’s certificate, common name and email address. If either of these parameters don’t match, a corresponding error is displayed. If the SSL read or write is interrupted prematurely (eg: client is closed), an error message is reported. Once the client sends its request and then receives a response from the server, the SSL socket is terminated by SSL_shutdown.