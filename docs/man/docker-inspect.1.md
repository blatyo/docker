% DOCKER(1) Docker User Manuals
% Docker Community
% JUNE 2014
# NAME
docker-inspect - Return low-level information on a container or image

# SYNOPSIS
**docker inspect**
[**--help**]
[**-f**|**--format**[=*FORMAT*]]
CONTAINER|IMAGE [CONTAINER|IMAGE...]

# DESCRIPTION

This displays all the information available in Docker for a given
container or image. By default, this will render all results in a JSON
array. If a format is specified, the given template will be executed for
each result.

# OPTIONS
**--help**
  Print usage statement

**-f**, **--format**=""
   Format the output using the given go template.

# EXAMPLES

## Getting information on a container

To get information on a container use it's ID or instance name:

    #docker inspect 1eb5fabf5a03
    [{
       "ID": "1eb5fabf5a03807136561b3c00adcd2992b535d624d5e18b6cdc6a6844d9767b",
       "Created": "2014-04-04T21:33:52.02361335Z",
       "Path": "/usr/sbin/nginx",
       "Args": [],
       "Config": {
            "Hostname": "1eb5fabf5a03",
            "Domainname": "",
            "User": "",
            "Memory": 0,
            "MemorySwap": 0,
            "CpuShares": 0,
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "PortSpecs": null,
            "ExposedPorts": {
                "80/tcp": {}
        },
	    "Tty": true,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
               "HOME=/",
	       "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/usr/sbin/nginx"
            ],
            "Dns": null,
            "DnsSearch": null,
            "Image": "summit/nginx",
            "Volumes": null,
            "VolumesFrom": "",
            "WorkingDir": "",
            "Entrypoint": null,
            "NetworkDisabled": false,
            "OnBuild": null,
            "Context": {
               "mount_label": "system_u:object_r:svirt_sandbox_file_t:s0:c0,c650",
	       "process_label": "system_u:system_r:svirt_lxc_net_t:s0:c0,c650"
	    }
        },
        "State": {
            "Running": true,
            "Pid": 858,
            "ExitCode": 0,
            "StartedAt": "2014-04-04T21:33:54.16259207Z",
            "FinishedAt": "0001-01-01T00:00:00Z",
            "Ghost": false
        },
        "Image": "df53773a4390e25936f9fd3739e0c0e60a62d024ea7b669282b27e65ae8458e6",
        "Labels": {
            "com.example.vendor": "Acme",
            "com.example.license": "GPL",
            "com.example.version": "1.0"
        },
        "NetworkSettings": {
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "Gateway": "172.17.42.1",
            "Bridge": "docker0",
            "PortMapping": null,
            "Ports": {
                "80/tcp": [
                    {
                        "HostIp": "0.0.0.0",
                        "HostPort": "80"
                    }
                ]
            }
        },
        "ResolvConfPath": "/etc/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/1eb5fabf5a03807136561b3c00adcd2992b535d624d5e18b6cdc6a6844d9767b/hostname",
        "HostsPath": "/var/lib/docker/containers/1eb5fabf5a03807136561b3c00adcd2992b535d624d5e18b6cdc6a6844d9767b/hosts",
        "LogPath": "/var/lib/docker/containers/1eb5fabf5a03807136561b3c00adcd2992b535d624d5e18b6cdc6a6844d9767b/1eb5fabf5a03807136561b3c00adcd2992b535d624d5e18b6cdc6a6844d9767b-json.log",
        "Name": "/ecstatic_ptolemy",
        "Driver": "devicemapper",
        "ExecDriver": "native-0.1",
        "Volumes": {},
        "VolumesRW": {},
        "HostConfig": {
        "Binds": null,
            "ContainerIDFile": "",
            "LxcConf": [],
            "Privileged": false,
            "PortBindings": {
                "80/tcp": [
                    {
                        "HostIp": "0.0.0.0",
                        "HostPort": "80"
                    }
                ]
            },
            "Links": null,
            "PublishAllPorts": false,
            "DriverOptions": {
                "lxc": null
            },
            "CliAddress": ""
        }

## Getting the IP address of a container instance

To get the IP address of a container use:

    # docker inspect --format='{{.NetworkSettings.IPAddress}}' 1eb5fabf5a03
    172.17.0.2

## Listing all port bindings

One can loop over arrays and maps in the results to produce simple text
output:

    # docker inspect --format='{{range $p, $conf := .NetworkSettings.Ports}} \
     {{$p}} -> {{(index $conf 0).HostPort}} {{end}}' 1eb5fabf5a03

    80/tcp -> 80

## Getting information on an image

Use an image's ID or name (e.g., repository/name[:tag]) to get information
 on it.

    # docker inspect 58394af37342
    [{
        "id": "58394af373423902a1b97f209a31e3777932d9321ef10e64feaaa7b4df609cf9",
        "parent": "8abc22bad04266308ff408ca61cb8f6f4244a59308f7efc64e54b08b496c58db",
        "created": "2014-02-03T16:10:40.500814677Z",
        "container": "f718f19a28a5147da49313c54620306243734bafa63c76942ef6f8c4b4113bc5",
        "container_config": {
            "Hostname": "88807319f25e",
            "Domainname": "",
            "User": "",
            "Memory": 0,
            "MemorySwap": 0,
            "CpuShares": 0,
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "PortSpecs": null,
            "ExposedPorts": null,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "HOME=/",
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/sh",
                "-c",
		 "#(nop) ADD fedora-20-dummy.tar.xz in /"
            ],
            "Dns": null,
            "DnsSearch": null,
            "Image": "8abc22bad04266308ff408ca61cb8f6f4244a59308f7efc64e54b08b496c58db",
            "Volumes": null,
            "VolumesFrom": "",
            "WorkingDir": "",
            "Entrypoint": null,
            "NetworkDisabled": false,
            "OnBuild": null,
            "Context": null
        },
        "docker_version": "0.6.3",
        "author": "I P Babble \u003clsm5@ipbabble.com\u003e - ./buildcontainers.sh",
        "config": {
            "Hostname": "88807319f25e",
            "Domainname": "",
            "User": "",
            "Memory": 0,
            "MemorySwap": 0,
            "CpuShares": 0,
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "PortSpecs": null,
            "ExposedPorts": null,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "HOME=/",
		        "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": null,
            "Dns": null,
            "DnsSearch": null,
            "Image": "8abc22bad04266308ff408ca61cb8f6f4244a59308f7efc64e54b08b496c58db",
            "Volumes": null,
            "VolumesFrom": "",
            "WorkingDir": "",
            "Entrypoint": null,
            "NetworkDisabled": false,
            "OnBuild": null,
            "Context": null
        },
	"architecture": "x86_64",
	"Size": 385520098
    }]

# HISTORY
April 2014, Originally compiled by William Henry (whenry at redhat dot com)
based on docker.com source material and internal work.
June 2014, updated by Sven Dowideit <SvenDowideit@home.org.au>
