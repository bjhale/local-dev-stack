# Simple, Flexible, Dockerized Local Development Environment

This is a docker local development stack that I have been using for a couple of years now. Its a group of dockerized services that allow web developers to spin up multiple projects in parallel with ease.

The environment consists of 3 elements:

* Traefik for a local proxy.
* Portainer for container management.
* Docker-gen for easy (less verbose) traefik configuration compatible with MOST use cases.

## Setup

### Windows

#### Pre-Requisites

    1. mkcert (Install with Chocolatey)
    2. WSL2 Setup with Ubuntu (or your choice) of distribution.
    3. Docker Desktop (Configured for WSL2 backend)

#### 1. Setup Local Certificates

This project uses localtest.me as an easy method to implement loopbacks without having to edit your hosts file.

Make sure you run these commands from a powershell command prompt, since mkcert needs to interact with your systems certificate store these commands will not function from a WSL terminal.

Install mkcert root certificates:

``` > mkcert -install ```

Install certificate for *.localtest.me:

``` > mkcert "*.localtest.me" -cert-file certs/_wildcard.localtest.me.pem -key-file certs/_wildcare.localtest.me-key.pem ```

#### 2. Expose daemon over TCP without TLS

As of writing this, mounting docker.sock as a volume is unreiable while using the WSL2 backend. As such, its less agravating to use the socket over TCP. Be aware this action has security implications.

#### 2. Setup .env

Copy .env.example to .env, uncomment the line for either Windows or Mac/Linux.

#### 3. Create Local Proxy Network

``` > docker network create local-proxy ```

or 

``` $ docker network create local-proxy ```

#### 3. Start The Stack

This command can be run from either the Windows terminal, or within you WSL terminal.

``` > docker-compose up -d ```

or 

``` $ docker-compose up -d ```

## Usage

Test your stack by visiting: https://whoami.localtest.me

Access portainer via http://localhost:9000

Access Traefik Dashboard via http://localhost:8080/dashboard/

See the whoami and whoami-easy services within docker-compose.yml for examples of how to configure your applications to utilize traefik.