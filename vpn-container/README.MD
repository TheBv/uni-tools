# VPN-Container
Permanent docker container based on https://github.com/ethack/docker-vpn

## Setup
Update .env file with your credentials


Add authorized ssh keys e.g. by using:
`run wget https://github.com/{username}.keys && mv {username}.keys authorized_keys`
or adding them manually.
These keys will be copied to the container allowing you to use it as a `JUMP_HOST` easily.

### Examples
### SSH-Config
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
  PubkeyAuthentication no #Optional but needed if you have too many ssh keys
```
## SOCKS5
#### Cloning/Managing Repositories 
```
git clone https://gitlab.texttechnologylab.org/repo --config 'http.proxy=socks5://127.0.0.1:1080'
```
We can also edit out .gitconfig file to proxy all urls matching the gitlab host domain:
```
[http "https://gitlab.texttechnologylab.org"]
	proxy = socks5://127.0.0.1:1080
```
#### SOCKS5 Setup(Firefox)

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