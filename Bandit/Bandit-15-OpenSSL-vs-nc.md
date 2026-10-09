# OverTheWire Bandit 15: When nc Isn't Enough

## Why I'm doing this
I'm rebuilding my Linux baseline from the ground up, broadening across topics and deepening in each one. OverTheWire Bandit is my structured path, and I'm writing up the levels that teach something worth keeping.

## The challenge
Level 15 asks you to submit the current password to a service on a local port, using an SSL/TLS-encrypted connection.

## What I did
I'd used `nc` (netcat) in the level before, but the prompt specifically required SSL/TLS, and nc only sends plain text. So I went with OpenSSL, a tool I hadn't had much reason to use before. Its `s_client` mode performs the TLS handshake with the server first, then lets you type into the connection the same way nc does.

## Why nc fails here
The service only speaks TLS. When nc connects and sends plain text, the server is expecting a handshake, so it can't make sense of what arrives. The protocol has to match before any data matters.

## TLS in plain terms
Transport Layer Security is a protocol that protects communication between two points. It encrypts the traffic so others can't read it, and it lets the client check it's talking to the right server.

## Where this shows up in real work
Any connection to a remote server or device, especially across networks you don't control: websites (HTTPS), email, APIs, and VPNs. Many organizations now encrypt internal traffic too, instead of assuming the internal network is safe.

## Takeaway
Read what the service expects before choosing your tool. The same goal, sending a password, needed a different tool because the protocol was different.
