# VPN-Container
Permanent docker container based on https://github.com/ethack/docker-vpn

## Use
Update .env file with your credentials


Add authorized ssh keys e.g. by using:
`run wget https://github.com/{username}.keys && mv {username}.keys authorized_keys`
or adding them manually.
These keys will be copied to the container allowing you to use it as a `JUMP_HOST` easily.

### Examples
```
# .ssh/config
Host vpn-Uni Uni
    Hostname 127.0.0.1
    User root
    Port 2222
    NoHostAuthenticationForLocalhost yes

Host eschar.hucompute.org
  HostName eschar.hucompute.org
  ProxyJump Uni
  User s0127943
  PubkeyAuthentication no
```
SOCKS5 Setup(Firefox)
`Settings > Network Settings > Settings... > Automatic proxy configuration URL > {File Path}`

```
# .ssh/firefox.pac
function FindProxyForURL(url, host){
    if ( dnsDomainIs(host,"gitlab.texttechnologylab.org") ) {
        return "SOCKS5 127.0.0.1:1080" ;
    }
	if ( dnsDomainIs(host,"isengart.hucompute.org") ) {
        return "SOCKS5 127.0.0.1:1080" ;
    }
}
```