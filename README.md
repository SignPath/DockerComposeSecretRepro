# Introduction

This reproduction sample shows a problem with mounting secret directories (as file mounting is not available for Windows containers) when using Docker Compose v2.

# Reproduction

This shows the respective outputs when running the reproduction sample Docker Compose v1/v2.

## Docker Compose v1

When running `docker-compose up` (aka Docker Compose v1) in the directory the following output is shown:
```
PS C:\Development\DockerComposeSecretRepro> docker-compose up
WARNING: Service "service" uses an undefined secret file "C:\Development\DockerComposeSecretRepro\Secrets", the following file should be created "C:\Development\DockerComposeSecretRepro\Secrets"
Creating network "dockercomposesecretrepro_default" with the default driver
Creating dockercomposesecretrepro_service_1 ... done
Attaching to dockercomposesecretrepro_service_1
service_1  | SUPER_SECRET
dockercomposesecretrepro_service_1 exited with code 0
```

## Docker Compose v2

When running `docker compose up` (aka Docker Compose v2) in the directory the following output is shown:
```
PS C:\Development\DockerComposeSecretRepro> docker compose up
[+] Running 1/2
- Network dockercomposesecretrepro_default      Created                                                           0.3s
- Container dockercomposesecretrepro-service-1  Creating                                                          0.0s
Error response from daemon: invalid mount config for type "bind": invalid mount path: '/run/secrets/C:\Secrets\'
```

This shows that secrets directories do not seem to work with Docker Compose v2.