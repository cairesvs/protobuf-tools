# Protobuf Tools

A docker image with protobuf and a handful set of plugins.

## Motivation

The whole idea is to provide an easy-almost-no-setup way to generate resources and documentation
from `proto`s.

## Dependencies

- Docker

## Content

This image gives you a compiled protobuf and some of its plugins (not so many for now):

- `protobuf3`: https://github.com/google/protobuf
- `protoc-gen-doc`: https://github.com/estan/protoc-gen-doc

## Usage

`docker run` with a couple options:

```sh
# Here we're inside your proto's folder, let's call it `my-protos`
cd ~/my-protos

docker run \
  -v `pwd`:/my-protos \
  -w /my-protos \
  -u `id -u $USER`:`id -g $USER`
  --rm -it brennovich/protobuf-tools:latest protoc --doc_out=html,index.html:doc *.proto
```

Let's take a close look, step-by-step:

1. ```-v `pwd`:/my-protos```: mounts the current directory into `/my-protos` inside the container;
2. `-w /my-protos`: set `/my-protos` as working directory, where your command will run;
3. ```-u `id -u $USER`:`id -g $USER````: ensures any manipulation of files to be done as a copy-cat of the
  host user, so we can't end up with undesired permissions;
4. `--rm -it brennovich/protobuf-tools:latest`: executes the given command in a container that will be removed
  immediately after the execution;
5. `protoc --doc_out=html,index.html:doc *.proto`: this command build docs in HTML format inside
  `~/my-protos/doc` for all `.proto` files.

## Contributing

1. Fork it
2. Fix, or add your feature in a new branch
3. Open up a Pull Request against this repo with an useful description
