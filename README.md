# OCI CLI Container 🚀

Run the [Oracle Cloud Infrastructure CLI](https://github.com/oracle/oci-cli) from a Docker or Podman container, without installing `oci-cli` directly on your host.

## ✨ What You Get

| Feature | Details |
| --- | --- |
| 🧰 OCI CLI included | Builds a local image with `oci-cli` installed |
| 🐳 Docker/Podman support | Choose your runtime from `env.mk` |
| 🔐 Host OCI config | Reuses your local `$HOME/.oci` configuration |
| 🌐 Proxy build option | Use `make oci-proxy` when a proxy is required |

## 📦 Project Files

| File | Purpose |
| --- | --- |
| `oci-cli_containerfile` | Container build recipe |
| `Makefile` | Build, update, and cleanup commands |
| `env.mk` | Runtime, version, revision, and proxy settings |

## 🛠️ Make Targets

| Command | Description |
| --- | --- |
| `make oci` | 🏗️ Build the OCI CLI container image |
| `make oci-proxy` | 🌐 Build the image using `HTTP_PROXY` from `env.mk` |
| `make oci-cleanup` | 🧹 Remove the local OCI CLI image |
| `make oci-update` | 🔄 Rebuild the image from scratch |

## 🚀 Quick Start

1. Edit `env.mk` and select your runtime:

   ```make
   RUNTIMECT=$(PODMAN)
   # RUNTIMECT=$(DOCKER)
   ```

2. Build the image:

   ```bash
   make oci
   ```

   If you need a proxy, set `HTTP_PROXY` in `env.mk` and run:

   ```bash
   make oci-proxy
   ```

3. Add an `oci` alias to your shell profile.

   For Podman:

   ```bash
   alias oci='podman run --rm -it --userns=keep-id -v "$HOME/.oci:$HOME/.oci:z" --tmpfs /run --tmpfs /tmp oci'
   ```

   For Docker:

   ```bash
   alias oci='docker run --rm -it -v "$HOME/.oci:$HOME/.oci" -v /sys/fs/cgroup:/sys/fs/cgroup:ro --tmpfs /run --tmpfs /tmp oci'
   ```

## ✅ Example

```bash
oci os ns get
```

```json
{
  "data": "mytenancy"
}
```

> 💡 Your OCI CLI configuration stays on the host under `$HOME/.oci`.

## 👤 Author

Ruggero Citton

## 📄 License

MIT License
