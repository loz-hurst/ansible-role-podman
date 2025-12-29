# ansible-role-podman

Ansible role for managing Podman

## Licence

Copyright 2025 Laurence Alexander Hurst

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.

## What it does

Installs [Podman](https://podman.io/) and setups users for root-less container usage (enables systemd linger and subuids/subgids).

Also provides `build-image` entry point for building images, with automatic fetching of base image and automatic updating if the base image is fetched or newer than the image to be built.

## Variables

The role uses these variables:

* `podman_users` - List of usernames (strings) to configure to use podman containers (default: empty list)
* `podman_user_subuid_range_size` - The size of new subuid ranges to create (int). (default: 65536)
* `podman_user_subgid_range_size` - The size of new subgid ranges to create (int). (default: 65536)

The `build-image` entry point uses these variables:

* `podman_image_build_user` - User to build the container as (string, required to discourage building as root)
* `podman_image_base_image` - Base image this image is to be built from (string, required)
* `podman_image_fetch_base` - Whether to fetch the base image or not, set to false if the base image should have already been built locally (boolean) (default: True)
* `podman_image_name` - Name of the image to build (string, required)
* `podman_image_container_file` - Containerfile contents as a string (string, required)
* `podman_image_build_args` - List of additional arguments, each item a dictionary with keys `name` (argument name) and `value` (argument value), to pass to the build process using `--build-arg` (string). (default: [])
